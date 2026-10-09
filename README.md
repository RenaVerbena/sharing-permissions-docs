# Sharing and permissions: UI guidelines

> **Published portfolio example.** Fieldstone is a fictional collaboration product. The feature, components, tokens, code APIs, owner roles, and review records in this repository are invented to show how UI guidelines can be structured, governed, and connected. Written by [Jorena Collins](https://github.com/RenaVerbena/RenaVerbena).

This repository documents the user interface of one feature: the Sharing and permissions panel, where people invite others to an item, change roles, share links, and remove access. It shows how component guidance, pattern guidance, and contributor standards fit together so that designers, engineers, writers, and the AI tools that draw on the documentation apply the same rules.

## The feature at a glance

The panel opens from the Share button on any item: a report, a dashboard, or a folder. It contains:

- A people picker and a role selector for inviting people.
- A list of everyone with access, each with a role and a row menu (Change role, Remove access).
- Link sharing controls: a switch for "Anyone with the link," the link's role, and Copy link.
- An ownership section, where the owner can transfer ownership.

### Vocabulary

One verb per action, used the same way in the interface, the help content, and the documentation.

| Term | Use for | Don't use |
| --- | --- | --- |
| Invite | Giving a person access | Add, Share with |
| Change role | Moving a person between roles | Edit permissions, Update access |
| Remove access | Taking a person's access away | Delete, Revoke, Unshare |
| Share link | Giving access through a link | Public link, Open access |
| Turn off link sharing | Ending access through a link | Revoke link, Disable |
| Transfer ownership | Making someone else the owner | Change owner, Reassign |
| Leave | Removing your own access | Remove myself, Unsubscribe |

| Role | What it allows |
| --- | --- |
| Viewer | Open the item |
| Editor | Change the item and invite viewers |
| Admin | Change roles and remove access |
| Owner | Everything above, plus transfer ownership and delete the item. One per item. |

## What's here

| Section | Answers the question | Page |
| --- | --- | --- |
| Components | What is this building block, how is it built, and how does it behave? | [Dialog](components/dialog.md) |
| Patterns | When and how do we combine components to do a specific job in this feature? | [Remove access confirmation](patterns/remove-access-confirmation.md) |
| Contributing | How do pages get written, reviewed, published, and kept current? | [CONTRIBUTING](CONTRIBUTING.md) |

## How the pages relate

Each page type has one responsibility, and the links between pages carry the relationship.

- A **component page** describes the building block once: anatomy, variants, states, behavior, accessibility, design assets, and the code API. It lists the patterns that depend on it under *Used in patterns*.
- A **pattern page** describes the job: when to use it, when not to, the flow, and the content. It links to the components it is built with under *Built with*, and it does not restate their behavior.
- When a component changes, its page changes, and *Used in patterns* says which pattern pages to check. When a pattern changes, the component is unaffected.

```
Remove access confirmation ──── built with ────▶ Dialog (alert variant)
            ▲                                           │
            └─────────── used in patterns ──────────────┘
```

This keeps a single source for each fact. A reader who lands on the pattern from search, the product's help link, or an AI answer gets the decision guidance and the content rules there, plus one link to the implementation details.

## Metadata and status

Every page starts with frontmatter. GitHub renders it as a table, and a docs site can use it for navigation, filtering, and search.

| Field | Purpose |
| --- | --- |
| `id`, `title`, `description` | Navigation and search |
| `tags` | Filtering across components, patterns, and features |
| `status` | `draft`, `in-review`, `published`, or `deprecated` |
| `owner` | The role accountable for the page (example roles) |
| `last_reviewed` | Date of the last completed review |
| `version` | The component or pattern version the page describes |

Status, owner, and review date are the same fields a documentation health report reads, so governance can be checked across the set without opening every page.

## Suggested reading order

1. [Remove access confirmation](patterns/remove-access-confirmation.md), to see guidance written around a decision the user makes.
2. [Dialog](components/dialog.md), to see the implementation detail the pattern relies on.
3. [CONTRIBUTING](CONTRIBUTING.md), to see how the two stay aligned over time.
