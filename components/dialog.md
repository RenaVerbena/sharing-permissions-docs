---
id: dialog
title: Dialog
description: A window layered over the page that interrupts the current task to ask for a decision or to present information the user must acknowledge.
tags: [component, overlay, dialog, accessibility, sharing-and-permissions]
sidebar_position: 1
status: published
owner: UI Platform team (example role)
last_reviewed: 2026-10-08
version: 2.3.0
---

# Dialog

> **Published portfolio example.** Fieldstone is a fictional collaboration product. The library asset names, tokens, props, versions, owner roles, and review records on this page are invented to show the structure of a component page.

| Document field | Value |
| --- | --- |
| Document ID | UI-COMP-014 |
| Component version described | 2.3.0 |
| Document owner | UI Platform team (example role) |
| Audience | Product designers, front-end engineers, content designers, and accessibility reviewers |
| Portfolio status | Published example |
| Example workflow status | Published |
| Review cycle | Each component release, and quarterly |

## Overview

A dialog is a window layered over the page. It stops the current task until the user responds, so use it only when the user must decide or acknowledge something before continuing.

In the Sharing and permissions panel, dialogs carry the decisions that change who can see or edit an item: confirming that someone's access will be removed, confirming a transfer of ownership, and inviting people when the invitation needs a message or a role choice.

**Use a dialog when** the user needs to confirm an action, make a choice that changes what happens next, or acknowledge information they must not miss.

**Don't use a dialog for** status updates that need no response (use a toast), long or multi-step forms (use a page or a drawer), or content the user may want to keep open while working (use a panel).

## Anatomy

```
┌──────────────────────────────────────────┐
│ Title                               [×]  │   1  Title
│                                          │   2  Close affordance (standard only)
│ Description                              │   3  Description
│ [Content slot]                           │   4  Content slot (optional)
│                                          │
│                  [Secondary]  [Primary]  │   5  Action bar
└──────────────────────────────────────────┘
               scrim behind the dialog          6  Scrim
```

1. **Title.** Required. One line that names the decision or the information.
2. **Close affordance.** Standard variant only. Dismisses the dialog without taking an action.
3. **Description.** Required. One or two sentences that say what the user needs to know to decide.
4. **Content slot.** Optional. Short form fields, a short list, or a summary. Not a place for long content.
5. **Action bar.** One primary action and one optional secondary action. The primary action is trailing.
6. **Scrim.** Dims the page and blocks interaction with it while the dialog is open.

## Variants

| Variant | Use for | Dismiss by scrim click or Escape | Close affordance |
| --- | --- | --- | --- |
| Standard | Choices and acknowledgments where leaving without acting is safe, such as an invitation with a message | Yes | Yes |
| Alert | Decisions with consequences, such as removing access or transferring ownership | No. The user must choose an action. | No |

### Sizes

| Size | Width | Use for |
| --- | --- | --- |
| Small | 320 px | A title, a description, and two actions |
| Medium (default) | 480 px | Short content in the content slot, such as a people picker or a verification field |
| Large | 640 px | A short form or a summary table |

Choose the size from the content. If the content needs more than Large, it belongs on a page or in a drawer.

## States

| State | Behavior |
| --- | --- |
| Closed | Not rendered. The trigger keeps focus. |
| Open | Rendered above the scrim. Focus is inside the dialog. |
| Action in progress | The primary action shows a loading indicator. All actions and dismissal are disabled until the action resolves. |
| Error | An inline message appears in the content slot. The dialog stays open so the user can retry or cancel. |

## Content

- **Title.** Sentence case, specific, and no longer than about 60 characters.
- **Description.** One or two sentences. Explain the outcome of the user's action.
- **Actions.** The primary action is a verb phrase that names the outcome. Never "Yes," "No," or "OK" alone. At most two actions in the action bar.
- **Vocabulary.** Use the feature terms in the [README](../README.md#vocabulary): Invite, Change role, Remove access, Transfer ownership, Leave.

Detailed content guidance for specific jobs lives on pattern pages, starting with [Remove access confirmation](../patterns/remove-access-confirmation.md).

## Behavior

- **Opening.** Focus moves into the dialog. The default is the first focusable element in the content slot, then the primary action. Alert dialogs should set `initialFocus` to the safer action.
- **While open.** The page behind the dialog is inert and does not scroll.
- **Closing.** Focus returns to the element that opened the dialog. A standard dialog closes on Escape, scrim click, the close affordance, or an action. An alert dialog closes only on an action.
- **Stacking.** Don't open a dialog from a dialog. If a second decision is needed, replace the content or finish the first dialog.

## Accessibility

Built into the component:

- `role="dialog"` for the standard variant and `role="alertdialog"` for the alert variant, with `aria-modal="true"`.
- `aria-labelledby` points to the title and `aria-describedby` points to the description, so screen readers announce both on open.
- Focus moves into the dialog on open and returns to the trigger on close. Tab and Shift+Tab stay within the dialog while it is open.
- The dialog surface, scrim, and action buttons use tokens that meet contrast requirements.

Required from the page or pattern that uses it:

- A visible, specific title. It is the accessible name of the dialog.
- Express everything needed to decide in the title and description.
- Don't rely on color alone to signal a destructive action. The label must say what happens.
- An alert dialog must offer a non-destructive action.

| WCAG 2.2 criterion | How it is met |
| --- | --- |
| 1.4.3 Contrast (Minimum), AA | Text on the dialog surface uses approved text tokens |
| 2.1.2 No Keyboard Trap, A | Focus is contained while open and released on close by keyboard |
| 2.4.3 Focus Order, A | Focus enters the dialog on open and returns to the trigger on close |
| 2.4.7 Focus Visible, AA | Focus ring tokens apply to all actions and the close affordance |
| 2.4.11 Focus Not Obscured (Minimum), AA | The dialog is centered above the scrim, and nothing covers the focused element |
| 2.5.8 Target Size (Minimum), AA | Actions and the close affordance meet the 24 by 24 CSS pixel minimum |
| 4.1.2 Name, Role, Value, A | Role, name, and description are exposed through ARIA |

Criteria that depend on how the dialog is used, such as 3.3.4 Error Prevention for removing access, are covered on pattern pages.

## Design notes

- **Library assets:** `Dialog / Standard` and `Dialog / Alert`, each with a Size property (Small, Medium, Large).
- **Tokens, by name:** `color.surface.overlay`, `color.scrim`, `radius.lg`, `elevation.3`, `space.inset.lg`, `space.stack.md`, `type.heading.sm`, `type.body.md`. Token values are defined in the Foundations guidelines and are not repeated here.
- If a design needs a value the tokens don't provide, propose a token change rather than detaching the component.

## Implementation notes

The API below is illustrative.

| Prop | Type | Default | Notes |
| --- | --- | --- | --- |
| `open` | boolean | `false` | |
| `variant` | `"standard"` or `"alert"` | `"standard"` | Alert disables scrim and Escape dismissal and hides the close affordance |
| `size` | `"sm"`, `"md"`, or `"lg"` | `"md"` | |
| `title` | string | required | The accessible name |
| `description` | string | required | The accessible description |
| `primaryAction` | `{ label, onClick, destructive?, loading? }` | required | `destructive` applies the destructive button style |
| `secondaryAction` | `{ label, onClick }` | none | Required when `variant` is `"alert"` |
| `initialFocus` | `"content"`, `"primary"`, or `"secondary"` | `"content"` | Use `"secondary"` for alert dialogs |
| `onClose` | function | none | Called after any dismissal. Focus restoration is handled by the component. |

```jsx
<Dialog
  open={isOpen}
  title="Invite the Finance group to Q3 forecast?"
  description="Everyone in Finance gets Viewer access. You can change roles or remove access later."
  primaryAction={{ label: "Invite Finance", onClick: invite }}
  secondaryAction={{ label: "Cancel", onClick: close }}
  onClose={close}
/>
```

## Used in patterns

| Pattern | Variant used | Status |
| --- | --- | --- |
| [Remove access confirmation](../patterns/remove-access-confirmation.md) | Alert | Published |
| Invite people | Standard | Planned |
| Transfer ownership | Alert, with typed verification | Planned |

## Related components

- **Button:** the actions in the action bar, including the destructive variant.
- **Toast:** feedback that needs no response, such as "Priya's role changed to Editor" with Undo.
- **Drawer:** longer tasks that still need the page context.

## Version history

| Version | Date | Change | Pattern pages affected |
| --- | --- | --- | --- |
| 2.3.0 | 2026-09-15 | Added the `initialFocus` prop and the alert-variant focus guidance | Remove access confirmation |
| 2.2.0 | 2026-06-02 | Added the Large size. Renamed the scrim token to `color.scrim`. | None |
| 2.0.0 | 2026-02-10 | Introduced the alert variant. Removed Escape dismissal from alert dialogs. | Remove access confirmation |

## Document governance

| Field | Value |
| --- | --- |
| Owner | UI Platform team (example role) |
| Required reviewers | Engineering (component API), Accessibility, Content Design |
| Last reviewed | 2026-10-08 |
| Next review | 2027-01-08, or the next component release |
| Propose a change | Follow [CONTRIBUTING](../CONTRIBUTING.md) |
