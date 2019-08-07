# welcome back!

## tldr

the team has been productive and positive. everyone is feeling good about the direction of the team,
having Kasia on board, and the work they're doing.

## new stuff

- We have our own repo, now: https://github.com/github/gitcoin-whiteglove . this has been pretty
  positive and blake/sam/brent are all happy with it. i audited every issue in the gitcoin repo and
  transferred everything for us over to the new repo. some issues still linger in `enterprise-web`
  though.
- Split up on-call rotations. We are splitting up self-serve and whiteglove on-call rotations. I
  will be writing docs up for us this week for the new whiteglove rotation.
- Ent Web docs. I documented everything in ent-web with screenshots and notes.
- Sales-ops project tracking doc: https://docs.google.com/spreadsheets/d/19VNPjUISnfiaj2rL1QZvqIsJBkFehx8M3vNcVDl69YQ/edit
- Separate board just for tracking issues (unsure if this is a good idea, still): https://github.com/orgs/github/projects/835
- team emoji :whiteglove:
- Whiteglove-specific reflections


## ongoing discussions

From my perspective the biggest ongoing discussion is dealing with **double-counting of email
invitations**. Sales ops requested that we count org invites as consuming a license, but unless it's
an org invite to a GH handle we currently can't know if the invited user is already licensed or not.
this is pretty serious and has caused a lot of headaches as SAML uses email invites to function.
i've recommended repeatedly that email invites shouldn't consume a license but for some reason sales
ops won't agree. Kasia agrees with me and is going to continue pushing for that with sales ops.

There have been a number of licensing headaches and need to do more work to improve the situation,
but the double counting of email invites is i think the most pressing issue.

Another discussion is around new internal **tooling for sales** to take advantage of. This tooling would
replace their Looker dashboard with custom reporting tools they can use when negotiating deals. The
current proposal is to house this in Enterprise Web while planning a sunsetting of ent-web's
customer-facing features.

The **education onboarding project** got heavily delayed by the cloud trials project, but it's being
worked on. We'll soon be blocked by design because designers forgot to assign anyone to our project
and haven't looked at it in two months. Kasia is staying on top of them.

The **multi-site readiness** stuff is almost ready to go; we're still waiting for the PCI cluster to
be fully ready but Sam took care of making our cron jobs resilient so all we have to do is tweak our
deployment config when the time comes.

## questions

- would you like to see the 1-1 notes i took while you were gone?
- anything i can do before i transfer that would be helpful?
