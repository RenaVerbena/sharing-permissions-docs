---
id: remove-access-confirmation
title: Remove access confirmation
description: How to ask for an explicit decision before removing a person's access, turning off link sharing, leaving an item, or transferring ownership.
tags: [pattern, dialog, content-guidelines, accessibility, sharing-and-permissions]
sidebar_position: 1
status: published
owner: Content Design (example role)
last_reviewed: 2026-10-08
version: 1.2.0
built_with: [dialog]
---

# Remove access confirmation

> **Published portfolio example.** Fieldstone is a fictional collaboration product. The examples, owner roles, versions, and review records on this page are invented to show the structure of a pattern page.

| Document field | Value |
| --- | --- |
| Document ID | UI-PAT-007 |
| Pattern version described | 1.2.0 |
| Document owner | Content Design (example role), with Product Design |
| Audience | Product designers, content designers, front-end engineers, and accessibility reviewers |
| Built with | [Dialog](../components/dialog.md) 2.3.0, alert variant |
| Portfolio status | Published example |
| Example workflow status | Published |
| Review cycle | Quarterly, and whenever Dialog changes |

## Overview

A remove access confirmation interrupts the user before an action that takes access away: removing a person from an item, turning off a shared link, leaving an item, or transferring ownership. It says who loses what, then asks for an explicit decision. It is built on the alert variant of the [Dialog](../components/dialog.md) component, so the user can't dismiss it by accident.

The goal is to help people understand the consequence while they can still change their mind, and to make the safe choice easy to find.

## When to use

- Removing a person's access to an item.
- Turning off link sharing when the link has been opened by anyone.
- Leaving an item, since the user loses their own access and can't get it back without an invitation.
- Transferring ownership, since the current owner gives up control.

## When not to use

- Changing a role. It's reversible, so apply it immediately and show a toast with Undo.
- Canceling a pending invitation. Nobody has access yet. Apply it and show a toast with Undo.
- Copying or regenerating a link when the old link keeps working.
- A settings page that already explains the consequence next to the control. Don't ask twice.

### Decision guide

| Question | If yes | If no |
| --- | --- | --- |
| Can the system undo it reliably within about 10 seconds? | Toast with Undo, no confirmation | Next question |
| Does someone lose access they can't restore themselves? | This pattern, with the impact stated | Next question |
| Does the user give up control of the item, as in transferring ownership? | This pattern, typed verification variant | This pattern, standard variant |

## The flow

1. The user starts the action from the panel: Remove access in a person's row menu, the link sharing switch, Leave, or Transfer ownership.
2. The confirmation opens as an alert dialog. Focus lands on the safe action.
3. The user chooses the removal action or Cancel.
4. On Cancel, the dialog closes and nothing changes. Focus returns to the control.
5. On confirm, the dialog shows the action in progress, then closes. The person's row leaves the list (or the link controls update), and a status toast confirms the result.

## Anatomy

| Part | Content | Component |
| --- | --- | --- |
| Title | Names the action, the person or link, and the item, as a question | Dialog title |
| Description | Who loses what, and anything they keep | Dialog description |
| Verification field (typed verification variant only) | The item's name, typed by the user | Dialog content slot |
| Primary action | Repeats the verb from the title. Destructive style. | Button, destructive variant |
| Secondary action | Cancel, or a label that names keeping the access | Button, secondary variant |

The alert variant has no close affordance and doesn't dismiss on scrim click or Escape. The user must choose.

## Content guidelines

### Title

- Name the action, the person or link, and the item, as a question.
- Keep it to one line, about 60 characters. Use the person's first name when it's unambiguous in the list, and the full name when it isn't.
- Don't ask "Are you sure?" It names no action and no person, and it reads as doubt instead of information.

| Do | Don't |
| --- | --- |
| Remove Priya from Q3 forecast? | Are you sure you want to remove this user? |
| Turn off link sharing for Q3 forecast? | Disable public link? |
| Leave Q3 forecast? | Remove yourself? |

### Description

- Say who loses what, in one or two sentences.
- State the scope when it's larger than the item the user clicked: linked dashboards, folder contents, people outside the organization.
- Say what the person keeps, when they keep something. It prevents a second question.
- Say once, in plain words, when the user can't undo it themselves.

| Do | Don't |
| --- | --- |
| Priya loses access to this report and its 3 linked dashboards. She keeps her own copies. | The selected user will no longer have access to this resource or any associated resources. |
| Anyone using the link loses access, including 12 people outside your organization. People you invited directly keep their access. | This will disable the link. |
| You'll lose access and will need an owner to invite you again. | You will be removed from this item. |

### Actions

- The primary action repeats the verb and names the person or the thing: "Remove Priya," "Turn off link sharing," "Leave report."
- Never "Yes," "No," "OK," or "Confirm." They force the user to re-read the title to know what they're agreeing to.
- The secondary action is "Cancel." When the safe choice benefits from being named, use it: "Keep access."
- Two actions only. If a third option exists, such as changing the role instead, it belongs in the row menu before the dialog opens.

| Do | Don't |
| --- | --- |
| Remove Priya / Cancel | Yes / No |
| Turn off link sharing / Keep link on | OK / Cancel |
| Leave report / Cancel | Confirm / Abort |

### Tone

- Plain and specific. No exclamation points and no alarm.
- Don't blame or lecture.
- Use a neutral, matter-of-fact tone appropriate for routine administration.
- Sentence case throughout.

## Variants

### Remove a person

Title, description, and two actions. Use for removing one person. The description names what they lose and what they keep.

### Turn off link sharing

Same structure. The description states how many people reached the item through the link, and whether any are outside the organization, because that's the fact the user is deciding on.

### Leave

The user removes their own access. Label the primary action "Leave," and use the description to say how to get access back. If the user is the owner, don't offer Leave. Offer Transfer ownership first.

### Transfer ownership, with typed verification

Add a text field that asks the user to type the item's name before the primary action enables, and say exactly what to type. The description states the user's new role after the transfer and that only the new owner can transfer it back. Use typed verification only here. The added friction suits a decision this consequential, and it wears out fast if it's overused.

### Remove several people

State the count in the title and the description: "Remove 4 people from Q3 forecast?" List names only when there are five or fewer.

## Accessibility

The Dialog component handles focus containment, labeling, and returning focus. This pattern adds:

- Use the alert variant. Its `alertdialog` role tells screen readers the dialog requires a response.
- Set initial focus on the safe action. A user who presses Enter out of habit shouldn't remove anyone.
- Carry the consequence in the label. The destructive button style reinforces it but can't be the only signal.
- Keep everything needed to decide in the title and description, which are the dialog's accessible name and description.
- Announce the result after the action completes, with a status toast, so the outcome isn't silent for screen reader users.

| WCAG 2.2 criterion | How the pattern meets it |
| --- | --- |
| 1.4.1 Use of Color, A | The consequence is carried by the label, not only by the button color |
| 2.4.3 Focus Order, A | Focus starts on Cancel and returns to the trigger on close |
| 3.3.4 Error Prevention (Legal, Financial, Data), AA | The removal is confirmed before it is committed, and the confirmation describes who loses what |
| 4.1.3 Status Messages, AA | The result is announced without moving focus |

## Design notes

- Library asset: `Dialog / Alert`. Size Small for Remove a person, Turn off link sharing, and Leave. Size Medium for Transfer ownership and Remove several people.
- Actions: `Button / Destructive` for the primary action and `Button / Secondary` for Cancel.
- No icon in the title. The question does the work.
- The destructive action is trailing in the action bar, matching the platform convention.
- The row menu lists Change role above Remove access, so the reversible option comes first.

## Implementation notes

An illustrative configuration using the Dialog API:

```jsx
<Dialog
  open={isOpen}
  variant="alert"
  size="sm"
  title={`Remove ${person.firstName} from ${item.name}?`}
  description={`${person.firstName} loses access to this report and its ${item.linkedCount} linked dashboards. ${person.pronounSubject} keeps ${person.pronounPossessive} own copies.`}
  primaryAction={{ label: `Remove ${person.firstName}`, destructive: true, onClick: removeAccess, loading: isRemoving }}
  secondaryAction={{ label: "Cancel", onClick: close }}
  initialFocus="secondary"
  onClose={close}
/>
```

After `removeAccess` resolves, close the dialog, remove the row, and show a status toast such as "Priya removed from Q3 forecast."

## Built with

- [Dialog](../components/dialog.md), alert variant, version 2.3.0 or later (for `initialFocus`)
- Button, destructive and secondary variants

## Related patterns

- **Change role (planned):** applied immediately, with Undo in a toast, instead of this pattern.
- **Invite people (planned):** the standard dialog with a people picker and role selector.
- **Transfer ownership (planned):** the typed verification variant, documented on its own once the flow ships.

## Version history

| Version | Date | Change |
| --- | --- | --- |
| 1.2.0 | 2026-09-22 | Moved initial focus to Cancel using Dialog 2.3.0 `initialFocus`. Added the Transfer ownership variant with typed verification. |
| 1.1.0 | 2026-05-14 | Added the Turn off link sharing and Remove several people variants, and the decision guide. |
| 1.0.0 | 2026-02-24 | First published version, on the Dialog 2.0.0 alert variant. |

## Document governance

| Field | Value |
| --- | --- |
| Owner | Content Design (example role) |
| Co-owner | Product Design |
| Required reviewers | Accessibility, Engineering |
| Last reviewed | 2026-10-08 |
| Next review | 2027-01-08, or when Dialog changes |
| Propose a change | Follow [CONTRIBUTING](../CONTRIBUTING.md) |
