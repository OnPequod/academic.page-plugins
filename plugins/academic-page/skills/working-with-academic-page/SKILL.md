---
name: working-with-academic-page
description: How to work on an Academic.page site through its tools - what each access level allows, what to do when a tool is missing, and how to edit records safely. Use whenever the user asks you to read, change, publish, or remove anything on their Academic.page site, such as their profile, location, bio, publications, positions, talks, pages, or courses.
---

# Working with an Academic.page site

## Check the access first

Call `key_show`. It names the site this connection works on and its access.
The tools you see depend on that access.

- **Edit your site** (the usual one) can change everything on the site except
  deleting: the profile and CV, publications, positions, degrees, links,
  talks, projects, courses, pages, posts, lab members, tags, navigation, and
  appearance. It can publish and unpublish.
- **Full access** can also delete. Anything deleted is kept for 30 days.
- **Read only** changes nothing.
- **Drafts only** is an older level. It may only create and edit drafts and
  build draft courses. It cannot publish or change anything visitors see,
  such as the profile, publications, positions, or degrees.

## When a tool you need is missing

The tool is missing because this connection's access does not include it.
Don't tell the user you have no tool for it. Tell them which access it needs,
and that they can change this agent's access on the AI agents page in
Academic.page, under the Connections tab, then start a new conversation.

With Edit your site, a request to remove something does not need Full access
when the record can be unpublished: unpublish it instead and say so. For
something with no published state, such as a position or a degree, tell the
user to delete it in the admin, or to give this agent Full access.

## Editing safely

- Read a record before you change it, and pass its `edit_version` with the
  update. A 409 `edit_conflict` means someone changed it since; read it again
  and redo the change.
- Rich text is Markdown: `bio_markdown`, `content_markdown`,
  `abstract_markdown`, and so on. Edit what you read and send it back.
- New posts, pages, talks, and courses are drafts unless you set
  `published_at` (`published` for projects). Publish only when the user asks.
- Changes to the profile, publications, positions, and degrees appear on the
  site as soon as they are saved. Say what you changed.
- Every tool accepts `dry_run=true` to preview a request without sending it.
  Use it before a large or unusual change.

## When you finish

Tell the user what you changed, what you left as a draft for them to review,
and anything you could not do with this connection's access.
