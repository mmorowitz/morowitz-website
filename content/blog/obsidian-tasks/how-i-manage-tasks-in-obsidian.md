---
title: How I Manage Tasks (and more) in Obsidian
description: A detailed explanation of using Obsidian as a daily journal and task manager.
date: 2023-01-28
tags:
---
Index:
1. [Overview](#overview)
2. [Core Setup](#core-setup)
    1. [Plugins](#plugins)
    2. [File Structure](#file-structure)
    3. [Templates](#templates)
        1. [The Daily Note Template](#the-daily-note-template)
        2. [The Person Template](#the-person-template)
        3. [The Project Template](#the-project-template)
3. [Workflow](#workflow)
4. [References and Other Reading](#references-and-other-reading)
5. [Changelog](#changelog)

## Introduction
I use Obsidian for a custom system that combines task management with daily journaling and free-form note taking. My goal was a balance between simplicity, flexibility, and portability. While this does utilize Obsidian-specific plugins, it doesn't *rely* on them to keep the information. Everything is still  markdown. Any plugin is essentially a shortcut/workflow enabler.

> **Note**: This guide covers templates and a workflow and assumes you know the basics of using Obsidian and plugins. I'm sure there are a thousand ways to improve this. If you have any questions, ideas, suggestions, or just want to say 'hi', I'm at hello at morowitz.com.

My task management workflow is loosely inspired by [David Allen's "Getting Things Done"](https://gettingthingsdone.com/), using concepts like *Next Action*, *Wating For*, periodic reviews, reminders (ticklers), and contexts.

The Obsidian system is driven by a few key components:
1. **Daily notes**: Each day has a note which is used for free-form journaling, task lists for today's relevant notes, and any other relevant daily information such as repeatable habits or checklists.

2. **Person notes**: Each person I interact with (primarily professionally) has a note (title prefixed with `@`). In this note I can display a list of tasks where they are mentioned and any other important information I need to remember about the person.

3. **Project notes**: Each project I'm working on has an index page which will house a list of tasks as well as any other project information (links to other notes, etc.)

4. **Tags and context lists**: Tasks are categorized by tags and viewable in lists based on context.

### System Overview
The system is driven by a Daily Note and its connections to People Notes and Project Notes.

- Tasks can be added anywhere, in any note, but they are primarily added to Daily Notes and Project Notes.
- A task gets added to a Daily Note in the context of taking notes during the day. If I think of something I need to remember tomorrow, I'll simply add the task in-line in the Daily Note and set the scheduled date for tomorrow.
- Tasks get added to project notes while project planning, during review cycles, or during other meetings, discussions related to the project.
- Daily Notes and Person Notes have queries which display lists of tasks associated with them.
    - In the case of Daily Notes, tasks are displayed which are scheduled for that day or earlier.
    - In the case of Person Notes, tasks are displayed which have a link to that note.
- There is a small risk of a task becoming an "orphan" (an untracked task with no date or tag). In general, a task should:
    1. Exist on a Project's main note so that it gets regularly reviewed
    2. Have an assigned date which will ensure it shows up on the appropriate Daily Note
    3. Have assigned tag, such as `#NextAction` or `#Context/Errand`
    4. Have a link to a Person Note
- Tasks can get also added to ad-hoc notes (e.g. meeting notes or other ephemeral documents). These notes get put, by default, in the Inbox folder to ensure they get reviewed before filing. This ensures that any tasks in those documents don't wind up as orphans in the system.
- Finally, there are root-level files that maintain broad queries of tasks which enable a larger review of the system or quick access to views across projects or people. These are:
    - **All tasks**: Self-explanatory.
    - **Next Actions**: All tasks tagged `#NextAction`. These are actionable tasks from projects. I review this daily.
    - **Waiting For**: All tasks tagged `#WaitingFor`. These are delegated tasks or tasks I'm waiting for someone else to complete. I review this daily.
    - **Context lists**: A list of all tasks tagged with whatever contexts I have. Since I work from home, I am not heavily context-driven. My most common context is `#Context/Errand`.
    - **Orphans**: This file should be empty at all times. It queries for tasks that are not in a Project or Person note, have no date, and have no tag. I check it regularly to make sure there aren't any tasks hiding in the system that I'm not aware of.

### Benefits of this system
- **Integrated**: The best part about this system for my use is that tasks live side-by-side with the information that they're related to. Other dedicated task managers are great at organizing complex lists of tasks but require management unto themselves, separate from the place where you take notes related to the actual work. This system allows both project note-taking, idea management, reminders, and tasks to be commingled.
- **Flexible**: I like that I can enter a task anywhere in the system, follow a few basic rules and feel comfortable that it's properly captured. I can create a note anywhere, at any time, and throw some in-line tasks in it and they'll be in my m.
- **Powerful**: The query language gives me the ability to look at any view of my tasks, embeddable in any note. For many task managers, this is a premium feature that you have to pay for.
- **Portable**: It's all in markdown files that I own. Yes, there are Obsidian plug-ins that power some of the viewing of tasks. But in the end, the tasks, tags, and links are all plain text. If Obsidian and all the plugins disappeared tomorrow, I'd still have all of my tasks.

### Downsides of this system
- It is technically possible for a task to get "lost". If I add a task without a #task tag or the wrong tags or without a date or in the wrong place, it could not show up where/when I need it to. This risk is mitigated by having a manual review process to go over my note edits for the day. Another mitigation technique is the "Orphan Notes" page in the root which queries for tasks that do not appear to be valid.
- Mobile capture isn't super simple. One of the benefits of dedicated task managers is that they're optimized for quick task capture with easy mobile apps/widgets. There is a "Quick Add" plugin which works nicely on desktop, but I don't have a capture problem on desktop. For now, I capture ideas on mobile in email and transfer to Obsidian during my daily review. I'm willing to live with this.
- It's kinda brittle. You've gotta write and maintain queries. Things can break. It's not an "off the shelf" solution. It takes some patience. This is not for everyone, but I enjoy the maintenance.
- Note templates are not "backwards compatible". By this I mean that if I update a query in a template, the notes that were generated from that template do not get that update. This isn't a huge problem for daily notes, but for Project Notes and Person notes, it's very annoying. There's no simple way for me to see how far a template has diverged from notes underneath it. The best way to solve is through complex search and replace or brute force editing sometimes.

## Core Setup
So, how do I set all this up? It's a combination of plugins, a vault structure, and some templates. Once all that is in place, there's a workflow that runs the show.

### Plugins
Besides the obvious installation of Obsidian, my system relies on the following plugins:
- [Tasks](https://github.com/obsidian-tasks-group/obsidian-tasks): Creates task creation and management tools.
- [Dataview](https://github.com/blacksmithgu/obsidian-dataview): Creates a system for querying your Obsidian vault and displaying the results in notes.
- [Archiver](https://github.com/ivan-lednev/obsidian-task-archiver): Enables easy archiving of completed tasks.
- Daily notes (core plugin): Makes it easy to create a daily note based on a template.
- Templates (core plugin): Enables the ability to use templates.
- [Templater](https://silentvoid13.github.io/Templater/): Enables a powerful language for embedding complex pieces of information in templates.

A few of other plugins are optional but make things a little easier:
- [Advanced Tables](https://github.com/tgrosinger/advanced-tables-obsidian): Makes it nice to build a table.
- [Calendar](https://github.com/liamcain/obsidian-calendar-plugin): A simple calendar widget that makes it nice to navigate between daily notes.

### Vault Structure

I started with a [PARA](https://fortelabs.com/blog/para/) structure, but modified it over time to fit my needs.

| Folder | Contains |
|--------| -------- |
| **Lists**   | Pages that display consolidated task lists (Next Actions, Waiting For, Contexts, All Tasks).
| **Inbox** | New random notes go here which gives me a central place to do a daily review |
| **Diary** | Daily notes go here. At the end of a month I group them in to a month subfolder and then a year subfolder. |
| **People** | People notes go here. I have a note for each person I interact with. This enables a quick view of tasks related to an individual when I talk to them.
| **Projects** | Each project has a main note and other sub notes, if necessary. Information about the project and project tasks go here |
| **Projects/Reminders** | I store lists of recurring task, one-off tasks, or reminders in files in this sub-directory. This is for everything that doesn't have a project associated with it or just a simple reminder. Examples include "Household Reminders", "Financial Reminders", "Birthdays & Anniversaries".
| **Reference** | A filing cabinet of notes I want to keep. Not related to task management. |
| **Archive** | I move old projects here and exclude this folder from the quick switcher via Obsidian settings.
| **Templates** | All templates go here.

### Templates
Templates are the heart of the system. They set up the Daily Note, Person Notes, and Project Notes

#### The Daily Note Template
Each day I generate a daily note. Here's a sample of a rendered daily note:

{% image "./dailynote.png", "A screen capture of a sample daily note from the sample vault" %}

This is generated from a sample Daily Note template ([source](https://github.com/mmorowitz/sample-obsidian-tasks-vault/blob/main/Templates/Daily%20Note%20Template.md)) which has three important task queries: Tasks Planned Today, Today's Reminders, and Tasks Completed Today.

##### Tasks Planned Today

This lists out any uncompleted tasks that have been either set to be DUE today (or earlier) or SCHEDULED today (or earlier). I do not personally use deadline, I simply review daily and schedule tasks.

 {% raw %}
 ```
(due before {{date:YYYY-MM-DD}}) OR (scheduled before {{date:YYYY-MM-DD}})
not done
path does not include Reminders
group by priority
```
{% endraw %}

Group by priority is my personal workflow preference. You can group or sort however you like. Another personal preference is that I exclude items in my "Reminders" folder from this task list and I pull them into a separate query below with the inverse path statement.

> **NOTE** This query relies a bit on using the [Global Task Filter](https://obsidian-tasks-group.github.io/obsidian-tasks/getting-started/global-filter/) feature of the Tasks plugin. Using this, I tag anything that is actually a task with a `#task` tag. The queries will ignore anything without that tag, enabling the creation of resusable checklists, such as my Daily Review or other shopping lists. If you don't use this, you have to put exclusion clauses in your queries by filename or by heading or some other method (this gets messy).


##### Today's Reminders
Same query as above, inverting the statement about the "Reminders" path. A personal preference to pull these separately.

{% raw %}
```
(due before {{date:YYYY-MM-DD}}) OR (scheduled before {{date:YYYY-MM-DD}})
not done
path includes Reminders
```
{% endraw %}

##### Tasks Completed Today
For my Daily Review, this provides everything completed on that day.

{% raw %}
```
done <% tp.file.title %>
hide due date
hide recurrence rule
hide done date
heading does not include Daily Review
```
{% endraw %}

This will show the completed task and what file it originated in.

Besides those queries, the rest of the content on the page is essentially supporting links and content that I might find useful during the day such as a Daily Review checklist. This changes relatively frequently.

#### The Person Template
I keep a note associated with each person I interact with. This may sound a little creepy at first, but all it really does is house a query of tasks where I mention that person. This could be done with tags (e.g. `#person/JohnDoe`) but you still have to house that query somewhere so I still needed the note.

Person notes are prefixed with a `@` to make it easy to filter when inserting a link or opening the file from the Obsidian quick switcher.

The Person note has two main uses:
1. Houses the query that shows all tasks where this person is tagged. So, when I'm talking to them, I can pull up a list of everything I want to discuss, review, or delegate to them.
2. Backlinks to this file serve as a record of when I met with an individual. I simply link to them in my Daily Note journal (see [sample vault](https://github.com/mmorowitz/sample-obsidian-tasks-vault)).

#### The Project Template
I keep a note associated with any project I'm working on. I use the [GTD definition of a project](https://gettingthingsdone.com/2017/05/managing-projects-with-gtd/): Anything that has multiple steps and a defined outcome.

I keep projects in a folder so I can group supporting notes with the parent project note. Project notes are prefixed with a `p-` to aid in filtering again. When a project is complete, it gets moved to the archive and the prefix changes to `a-`.

> Tip: If you have a lot of projects, frontmatter fields are useful at the index note to allow for a dataview query to build different project lists for you. Sometimes I use this method, sometimes I don't. It depends on my workload.

Project notes have the following uses:
1. Hold tasks related to the project.
2. Backlinks to the note, generally originating in Daily Notes, will show a history of my time spent on the project.
3. Other notes, external links, or general information is indexed on the project note.

## Workflow
1. At the end of the day, I do my "Daily Review" checklist which includes:
    - Emptying all my inboxes and creating any necessary tasks
    - Reviewing the current day's notes and new tasks and updating as needed
    - Reviewing all open projects and their tasks and updating as needed
    - Choosing tasks for the next day from #NextActions. I mark those tasks as scheduled for the next day using the tasks plugin.

2. When the review is done, I generate the Daily Note for the next day and review the tasks I assigned as well as the reminders that have been created for that day. Then, I set priorities for the day. I use a 2+n method of prioritization: Two tasks that absolutely MUST get done (high priority) and *n* (up to 8 or 10) that I could work on (medium priority + reminders for the day).

3. I set up my journal for the day by putting placeholder headings in the Daily Note for big meetings and pre-linking them to People and/or Project notes. I pin the next day's note and close the current day.

There are definitely efficiencies that can be found with more advance uses of plugins, Templater, and other tips and tricks. The possibilities are pretty vast. If you have some suggestions, ideas, questions, or just want to say 'hi' or thanks, you can reach me at hello at morowitz.com.

## References (and other reading)
- [My sample Obsidian vault](https://github.com/mmorowitz/sample-obsidian-tasks-vault)
- [David Allen's "Getting Things Done"](https://gettingthingsdone.com/)
- [Tiago Forte's PARA Method](https://fortelabs.com/blog/para/)
- [Obsidian Tasks Plug-In](https://obsidian-tasks-group.github.io/obsidian-tasks/)

## Changelog
2023.02.25: Formatting updates, spelling fixes, and some links added

2023.01.28: Initial Version
