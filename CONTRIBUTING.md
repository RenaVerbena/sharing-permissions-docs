# Contributing to the Sharing and permissions guidelines

> **Published portfolio example.** The roles, review steps, and tooling here are fictional and simplified to show a contribution model.

Anyone who works on the feature can contribute: product designers, engineers, content designers, accessibility specialists, support, and product managers. You don't need to be on the UI Platform team or the Content Design team. You do need to use the page templates and follow the review workflow, so the guidelines stay consistent and people can trust what they find.

## Page types

Pick the page type by the question the reader is asking.

| Reader's question | Page type | Owner |
| --- | --- | --- |
| What is this building block, and how does it behave? | Component page | UI Platform team |
| When and how do we use components to do a job in this feature? | Pattern page | Content Design, with Product Design |
| What words and roles does the feature use? | Feature overview (the README) | Content Design |

## Templates

### Component page

1. Frontmatter (see Metadata)
2. Overview, with the one-sentence rule for when to use it
3. When to use and when not to use (short; patterns hold the detail)
4. Anatomy
5. Variants and sizes
6. States
7. Content
8. Behavior
9. Accessibility
10. Design notes (library asset names and tokens by name)
11. Implementation notes (props, events, and a minimal example)
12. Used in patterns
13. Related components
14. Version history
15. Document governance

### Pattern page

1. Frontmatter
2. Overview
3. When to use and when not to use, with a decision guide if the choice isn't obvious
4. The flow
5. Anatomy (which components, in which configuration)
6. Content guidelines, with do and don't examples
7. Variants
8. Accessibility (only what the pattern adds beyond its components)
9. Design notes
10. Implementation notes (a configuration example, not an API reference)
11. Built with
12. Related patterns
13. Version history
14. Document governance

## Metadata

Every page needs `id`, `title`, `description`, `tags`, `status`, `owner`, `last_reviewed`, and `version`. Pattern pages also list `built_with`.

| Status | Who sets it | Meaning |
| --- | --- | --- |
| `draft` | Any contributor | Work in progress. Not linked from navigation. |
| `in-review` | The contributor, when the pull request is opened | Reviews requested. |
| `published` | The page owner | Reviewed and current. |
| `deprecated` | The page owner | Kept for reference. The page names its replacement. |

## Writing standards

- Use the feature vocabulary in the README. If the interface and the documentation disagree on a word, fix the one that's wrong and record the decision in the vocabulary table.
- Lead with the decision. Say when to use and when not to use before explaining how.
- Keep warnings and prerequisites next to the step they affect.
- One source for each fact. Patterns link to components for behavior and API details. If you find yourself restating how a component behaves, link instead.
- Give every content guideline a do and a don't example, using the feature's own objects: reports, dashboards, folders, people, links.
- Use link text that says where the link goes.
- Sentence case for headings, titles, and labels. Plain words over system jargon.
- Write for the reader who arrives mid-page from search or an AI answer. Each section should make sense with its heading and one link back to context.

## Review workflow

1. **Propose.** Open an issue that describes the page or change, the reason, and the components or patterns it affects. The owner confirms scope within a week.
2. **Draft.** Work on a branch using the template. Set `status: draft`.
3. **Review.** Open a pull request, set `status: in-review`, and request:
   - Product Design for accuracy against the design library and the current panel
   - Engineering for accuracy against the coded component
   - Accessibility for any page with an Accessibility section or a behavior change
   - Content Design for clarity, voice, vocabulary, and the content guidelines
4. **Publish.** The owner merges, sets `status: published`, updates `last_reviewed` and `version`, and adds a Version history entry.
5. **Maintain.** Every page is reviewed quarterly, and whenever the component it describes or depends on ships a change.

### Decision rights

| Decision | Decides | Consulted |
| --- | --- | --- |
| Add a component page | UI Platform lead | Engineering, Accessibility |
| Change content guidelines or vocabulary | Content Design lead | Product Design, Support |
| Deprecate a page | Page owner | Owners of pages that link to it |
| Publish a page | Page owner | Required reviewers |

## Keeping pages aligned with releases

When a component ships a change:

1. Update the Behavior, Accessibility, Design notes, and Implementation notes sections.
2. Bump `version` and add a Version history entry that names the pages affected.
3. Open each page listed under *Used in patterns* and check whether the pattern's configuration, focus behavior, or content guidance still holds.
4. Note the documentation changes in the component's release notes.

When the panel ships a change to a label, a role, or a flow, update the README vocabulary first, then the pattern pages that use the changed term. When a token is renamed, search the documentation for the old name before publishing.
