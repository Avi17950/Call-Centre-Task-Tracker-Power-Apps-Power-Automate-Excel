# Call-Centre-Task-Tracker-Power-Apps-Power-Automate-Excel
A task tracker for a technical-support call centre handling truck and bus roadside and workshop queries. Built as a Power Apps canvas app over an Excel workbook in OneDrive, with two Power Automate flows for notifications
Built as a working reference: every formula here has been run in a real environment, including the fixes for the places where the Excel connector behaves differently from SharePoint or Dataverse.

**What it does**
Lists every task with search, a status filter and a team filter
Flags overdue tasks in red on the list
Add, edit and delete tasks through a form with dropdowns and date pickers
Dashboard with counts by status and open tasks per team
Team screen showing open and overdue counts per person
Emails the assignee automatically whenever a task is saved
Emails the team manager every morning with the overdue list

**Screenshots**
Task list

Task list screen with the team filter open

The gallery sorted by due date, with keyword search, a status filter and a team filter. Overdue tasks are flagged in red automatically — a task counts as overdue when its due date has passed and its status is anything other than Completed. Status text is colour-coded, and each row resolves the stored email address to the person's display name.

Built in Power Apps Studio

The same screen in Power Apps Studio, showing the control tree

The control tree for TaskListScreen. All three tables — Tasks, Members and Teams — are connected through the Excel Online (Business) connector; the gallery filters and sorts locally because the Excel connector does not delegate.

**Architecture**

Excel workbook (OneDrive for Business)
  ├── Tasks    table  — the records the app reads and writes
  ├── Members  table  — people, roles, emails (reference data)
  └── Teams    table  — queues and their team lead (reference data)
            │
            ▼
Power Apps canvas app  (4 screens)
  ├── TaskListScreen   — gallery, search, filters, overdue flag
  ├── TaskEditScreen   — edit form, dropdowns, date pickers
  ├── DashboardScreen  — status counts, pie chart, column chart
  └── TeamScreen       — per-person workload
            │
            ▼
Power Automate
  ├── Notify Task Assignee        — instant, called from the app on save
  └── Daily Overdue Task Reminder — scheduled 09:00 daily
