# FCAJ Frontend Page Templates

> Quy ước template để implement nhất quán trong React SPA. Đây là mẫu cấu trúc/behavior, không phải mã ứng dụng chạy độc lập.

## A. Public discovery template

```text
AppShell
├── PublicHeader (logo, Events, About, account action)
├── MainContainer
│   ├── PageIntro (title, short description, optional primary CTA)
│   ├── FilterBar (only server-supported filters; URL-backed)
│   ├── EventGrid
│   │   └── EventCard (date/time, title, location, status, CTA)
│   ├── Pagination
│   └── Loading | Empty | Error state
└── PublicFooter
```

Behavior: request paginated events; abort stale requests; preserve filters in query string; never infer total count from loaded page. Empty state offers clear filters or browse again.

## B. Event detail template

```text
AppShell
├── Breadcrumbs
├── EventHero (title, status, dates, location)
├── Main + Aside
│   ├── Description
│   ├── PublicProgram (approved submissions only)
│   └── Aside: Capacity/deadlines + ParticipationPanel
└── RegistrationDialog | CFP route
```

ParticipationPanel is rendered from `viewer.participation`, `can_manage`, event dates/status and returned counters. For attendee, show register/cancel if allowed. For speaker, link to submission detail/apply. Registration and CFP never share a fake generic “approval” state.

## C. Auth form template

```text
CenteredAuthLayout
├── Brand + concise task heading
├── FormCard
│   ├── FieldGroup(s) with persistent labels
│   ├── Inline validation summary
│   ├── Primary submit (pending state)
│   └── Alternate auth links
└── PageAlert (email sent, expired link, suspended, etc.)
```

Use existing auth routes and response contract. Never expose whether an email exists where the backend intentionally returns generic responses.

## D. My participation template

```text
AppShell
├── PageIntro
├── Tabs: Attending | Speaking
├── Filter/status chips (valid for current domain only)
├── ParticipationList
│   └── EventParticipationCard (event + type-specific state + next action)
└── Loading | Empty | Error | Pagination
```

Fetch `/me/registrations` and `/me/speaker-submissions` independently. Preserve their distinct statuses; merge only for visual chronology if pagination semantics remain honest. Attendee card does not show pending/rejected; speaker card can.

## E. Speaker submission form/detail template

Form sections: event/topic, abstract, tags, duration, bio, private note to admin, presentation file. Detail shows status, review note where allowed, file state, edit/withdraw availability, and event context. File upload sequence: initialize API → direct presigned PUT → complete API → refresh submission. Handle expiry, failed PUT, complete conflict, superseded/deleted file.

## F. Admin shell and data page template

```text
AdminShell
├── Sidebar / mobile drawer
├── Topbar (breadcrumb, account)
└── Content
    ├── PageHeader (title, contextual CTA)
    ├── FilterToolbar
    ├── DataTable / responsive cards
    ├── Pagination
    └── Loading | Empty | Error
```

Use for events, review queue, attendees, users, and notifications. Use server pagination and role guards. Do not introduce global KPI cards without a defined API/data source.

## G. Admin event detail/form template

Event form grouped as: basics, date/timezone, location, capacity, attendee deadlines, CFP window/material deadline, speaker cap. Validate relationships in the browser for speed; show backend field errors as final authority. Event detail actions: edit, publish, cancel, delete draft only, attendees, notification summary. Destructive actions require explicit confirmation.

## H. CFP review template

Queue: event/status filters, applicant/topic/status/file indicator, pagination. Detail: applicant and proposal, private file download, approve action, reject form with required review note. On conflict (speaker cap/event changed), keep reviewer context and explain refresh/retry. Never display admin-only note in public program.

## I. Account and notifications template

Account profile fields and password action; notification preference list with explicit save feedback. Keep account preferences separate from platform admin settings. Unsubscribe route handles the signed token from email and shows outcome without requiring login.

## Shared states / route policy

Every data route defines: skeleton, empty, failed/retry, not found, forbidden, and stale/mutation conflict behavior as applicable. Route gates are authorization UX only; server authorization remains decisive. Unknown API enum values render a neutral fallback. Query mutations invalidate or refetch the affected entity/list.

## Suggested reusable component inventory

- `AppShell`, `PublicHeader`, `AdminSidebar`, `PageHeader`, `Breadcrumbs`
- `Button`, `IconButton`, `TextField`, `SelectField`, `TextArea`, `DateTimeField`, `FileDropzone`
- `Card`, `Badge`, `Alert`, `ToastProvider`, `ConfirmDialog`, `Modal`, `Tabs`, `Pagination`
- `EventCard`, `EventStatusBadge`, `RegistrationStatusBadge`, `SubmissionStatusBadge`
- `EmptyState`, `LoadingState`, `ErrorState`, `DataTable`, `ResponsiveList`

Use existing project components where they meet this contract; rebuild only where needed rather than duplicating primitives.
