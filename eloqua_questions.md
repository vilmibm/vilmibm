# questions related to [mike's gist](https://gist.github.com/mike421453/3716550d00335cc527b66d4c5d7c30bc)

- [x] Design calls for anything submitted to trial/contact forms be persisted in EntWeb's database. Does the current Contact model suffice for that?
 - **we're not going to persist at all***
- [x] Once we've saved a contact request entry, will it ever change?
  - looks like we want replayable events, so it will at least need a mutable "sent" field, but other than that?
  - **covered by job retrying as needed**
- [x] Do we want a separate notion of "contact" vs. "contact request"? or does the former just exist wholly in Eloqua?
  - **Contact model is placeholder to queue up job for submitting to salesforce, we can reuse it**
- [x] For the "Eloqua processing" section, are those things that we're setting up? or that Eloqua does for us already?
  - **managed by marketing ops, we don't have to implement that**
- [x] Failure to submit to Eloqua should "notify parties" -- is there a process in place for that? Open an issue in a repo? Who gets notified?
  - **ignore for now**
- [x] it's okay to submit to eloqua in a job?
  - **yes**
- [x] should we hardcode the eloqua form ID? do we expect it to change much? I'm assuming forms are created by hand, not per submission or anything.
  - **form id in env var; lib/enterprise, lib/github**
  - What about form field ids? should we hardcode those?
  - **-> definitely ask mike about this. probably shove into yml file. hopefully can get away with just storing htmlName**
  - we could fetch and cache form field ids, but need a consistent mapping to fields in our form/model.
  - **-> Need a staging form**
- [x] when checking for form data, can we specify a form data ID? Eloqua's docs say no, you just have to get back a list of form data for a given form ID.
  - **i don't think we need to do this**
- [x] My assumption is that ent-web is solely acting as a collection point for this data and that it will be viewed in Eloqua or SFDC, is that correct?
  - **yes**

# composition sketch

- `ContactRequest`
  - Either a replacement or renaming of our current `Contact` model
  - Backing model for the `/trial` and `/contact` forms
- `EloquaForm`
  - has hardcoded field values, form ID stored as class instance variables
  - `self.build_from_contact_request` 
    - Given an instance of `ContactRequest`, returns a filled-in `EloquaForm`.
  - `valid?`
    - Ensures that any payload conforms to the field values set up in Eloqua. This should be used prior to submitting in case the data was fudged (perhaps from a repl or similar) prior to calling `submit`
  - `submit`
    - Assuming `valid?` passes, submits this instance's payload to Eloqua. If successful, updates the associated `ContactRequest` with `submitted: true` or similar. If false, raises `EloquaPostException`
- eloqua submission job
  - Given some `ContactRequest` ID, creates and submits an `EloquaForm`.
  - Catches `EloquaPostException` and schedules retries as needed
- `EloquaPostException` 
  - Raised when any REST POST to Eloqua fails.
