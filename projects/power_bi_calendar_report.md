# Power BI report from Calendar events (Power Automate, Graph API, SharePoint Online, Power Query, Power BI)

power-bi-report-from-calendar-events-power-automate-graph-api-sharepoint-online-power-query-power-bi)

*Back to [Projects](https://camilovillam.github.io/#power-bi-report-from-calendar-events-power-automate-graph-api-sharepoint-online-power-query-power-bi).*

## Description

A Power BI report of calendar events and meetings. Data is extracted from the Graph API and loaded in raw JSON files in SharePoint Online. Transformation, data modeling and visualization are done in Power Query and Power BI.

## Features

- Power BI report with different pages, bookmarks and consistent cross-filtering across visuals and pages.
- Event and meeting analysis for decision-making, including number of meetings, organizations, targets, scheduling, partipants, time trends, among others.
- Clean design while following look and feel of the client.
- Automatic data extraction and report refreshes 8 times per day.
- Complete data pipeline orchestrated by Power Automate.

## Technologies and tools

- Power Automate
- Power Query
- Power BI
- SharePoint Online
- Graph API (Pagination and Delta links)

## Year

2025

## Power Automate Data flow:

A Power Automate flow runs scheduled every three hours to extract Outlook calendar events using Microsoft Graph API. It fetches only new or modified events (using Delta links) within a date range of -30 to +180 days from today. The events are saved as JSON files in a specific OneDrive folder. If any errors occur, the flow sends notification emails and updates a Power BI dataset. The flow also manages configuration and backup files to track changes and ensure data consistency.

### 1. Ingestion
Trigger: Scheduled recurrence starts the flow.
Source: Outlook calendar events are fetched via Microsoft Graph API.

### 2. Processing
Filtering: Only new or modified events are retrieved using Delta tokens.
Transformation: Events are formatted as JSON objects.
Pagination: Handles large datasets by looping through pages.

### 3. Storage
Output: Events are saved as JSON files in a OneDrive folder.
Config Management: Delta tokens and sequence numbers are stored/updated in a config file.

### 4. Error Handling & Notification
Monitoring: Flags errors and sends notification emails if failures occur.
Backup: Backs up config files before updates.

### 5. Reporting
Power BI: Refreshes a Power BI dataset to update reports with the latest calendar data.

###6. Orchestration
This flow automates the end-to-end pipeline: data extraction, transformation, storage, error management, and reporting.



## Screenshots

- Power BI report - Overview page:

![Power BI calendar report - Overview](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_01.png?raw=true)

- Participants page:

![Power BI calendar report - Participants](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_02.png?raw=true)

- Recurring meetings page:

![Power BI calendar report - Recurring](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_03.png?raw=true)

- Scheduling analysis:

![Power BI calendar report - Participants](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_04.png?raw=true)

- Time trends analysis:

![Power BI calendar report - Time trends](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_05.png?raw=true)

- Power Automate flow - Delta Link:

![Power Automate flow - Delta Link](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_06.png?raw=true)

- Power Automate flow - Pagination:

![Power Automate flow - Pagination](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Calendar_report_06.png?raw=true)



*Back to [Projects](https://camilovillam.github.io/#power-bi-report-from-calendar-events-power-automate-graph-api-sharepoint-online-power-query-power-bi).
