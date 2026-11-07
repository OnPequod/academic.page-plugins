---
name: course-from-syllabus
description: Set up a course on Academic.page from a syllabus, with its lessons, readings, and assignments. Use when the user gives a syllabus or course outline and asks to create or build the course on their site.
---

# Build a course from a syllabus

Any access but Read only is enough. Keep the course a draft unless the user
asks you to publish it, so they can review it first.

## Steps

1. Call `key_show` and `site_get`. Courses belong on a course site, or on a
   personal site that uses courses. Check `courses_list` for a course that
   already matches, and ask before adding a second one.
2. Upload the syllabus file with `media_upload`, sending it as
   `content_base64` with its `filename`. Files over 8 MB go through
   `media_multipart_init`, `media_multipart_sign`, and
   `media_multipart_complete`.
3. Create the course with `courses_create`, passing `syllabus_media_id` from
   the upload. Fill in `title`, `instructor_name`, `primary_institution`, and
   the description in `content_markdown`. Add the offering in `instances`,
   with `course_number`, `term`, `year`, `starts_on`, and `ends_on`.
4. Add a lesson for each week or session with `course_lessons_create`, in
   order, with its `title` and an `overview` of the topic.
5. Add the readings with `course_references_create`, setting `kind`,
   `title`, `authors`, and `details`. Add the assignments with
   `course_assignments_create`, with `due_date` and the `lesson_id` they
   belong to.
6. Read the course back with `courses_get` and compare it with the syllabus.

## When you finish

Tell the user the course is a draft, list what you added, and point out
anything in the syllabus you were unsure about, such as a missing date or an
unclear reading. They review it in the admin and publish it there.
