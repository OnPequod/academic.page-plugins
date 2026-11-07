---
name: add-cv-to-site
description: Add the publications, talks, positions, and degrees on a CV to the person's Academic.page site. Use when the user gives a CV, resume, or list of their work and asks to put it on their site, fill in their site, or bring their site up to date.
---

# Add a CV to an Academic.page site

Work from what the site already has, add only what is missing, and tell the
user what you added and what you left for them.

## Before you start

1. Call `key_show`. It lists the sites this connection reaches and its access.
   A CV belongs on the personal site, the default when you pass no `site_id`.
   - **Edit your site** or **Full access** can add everything on a CV.
   - **Read only** changes nothing. Compare the CV with the site and report
     what is missing.
   - **Drafts only**, an older level, can add talks and projects as drafts
     but not publications, positions, or degrees. Tell the user they can
     change this agent to Edit your site on the AI agents page in
     Academic.page (Connections tab) and start a new conversation, or offer
     to add only the talks.
2. Read what the site has: `profile_get`, `profile_positions_list`,
   `profile_degrees_list`, `publications_list`, and `talks_list`.

## Publications

- Prefer a BibTeX file if the user has one, such as a Google Scholar export.
  Call `publications_import` with `dry_run=true` first and show the user the
  entries and their status. Import only once they agree.
- Otherwise add each publication from the CV with `publications_create`,
  keeping the default `on_match=skip`. A 409 means the site already has it,
  or may: note the match and move on. Do not send `create_anyway` unless the
  user confirms the entry is a separate work.
- Include the DOI whenever the CV gives one. The site checks each DOI against
  its published record and saves any difference as a suggestion. See the
  check-publications skill.
- Keep the CV's order within each year with `year_order`, top of the year
  first.

## Talks, positions, and degrees

- Add talks with `talks_create`. They start as drafts. Set `talk_date`,
  `meeting_name`, `location`, `talk_type`, and `copresenters` where the CV
  gives them. Keep the CV's order within each year with `year_order`.
- Add positions and degrees with `profile_positions_create` and
  `profile_degrees_create`.
- Skip anything the site already lists, even if the wording differs slightly.
  Ask the user when you are unsure whether two entries are the same.

## When you finish

Tell the user what you added, by kind and count, what you skipped as already
there, and what you could not add with this connection's access. Publications,
positions, and degrees appear on the site at once. Talks you added are drafts
unless the user asked you to publish them: they can review and publish them in
the admin.
