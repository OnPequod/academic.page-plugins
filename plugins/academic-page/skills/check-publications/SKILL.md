---
name: check-publications
description: Check the publications on an Academic.page site against their published records, such as DOIs, and fix authors, venues, years, and other details. Use when the user asks to check, verify, clean up, or correct their publications or citations.
---

# Check publications on an Academic.page site

Academic.page compares each publication that has a DOI with its DOI record.
When they differ, the difference waits as a suggestion and the citation does
not change until someone accepts it. Your job is to work through those
suggestions with the user, and to find what the site cannot check on its own.

## Steps

1. Call `key_show`. Changing publications needs Edit your site or Full
   access. With Read only or Drafts only, report what you find and tell the
   user they can change this agent to Edit your site on the AI agents page in
   Academic.page (Connections tab), then start a new conversation.
2. Call `publications_list` and read each publication's `suggestion`. A
   suggestion lists each difference in `changes`.
3. For each suggestion, show the user the differences in plain words, such
   as "The DOI record lists the volume as 12; the site says 11."
   - To accept all of it, call `publications_apply_suggestion` with the
     publication's `edit_version`.
   - To accept one field, pass `field`, such as `volume`.
   - To keep the citation as it is, call `publications_keep_citation`. The
     same suggestion is not offered again.
4. For publications without a DOI, look for one in the published record and
   add it with `publications_update`. The site then checks it and may offer a
   suggestion of its own.
5. Look for duplicates, such as a preprint and its published version, and
   ask the user which to keep before deleting anything.

## Rules

- Change a citation only when the published record supports it, and say
  where it came from.
- Send the `edit_version` you read. A 409 `edit_conflict` means someone saved
  the publication since: read it again and redo the change.
- Anything deleted is kept for 30 days. Still, ask before deleting.
