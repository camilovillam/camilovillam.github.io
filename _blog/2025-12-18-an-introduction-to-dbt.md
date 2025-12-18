---
layout: blog
title: An Introduction to dbt - Transforming Calendar Data for Analytics
date: 2025-12-18
author: Camilo Villa
---

> _“This meeting should have been an email”._

We’ve heard this. We’ve said this. We’ve thought about this.

How much time do we spend in meetings? How many meetings do we have in a year? Are we _really_ drowning in meetings, as we all seem to think? Should we make [**better use of our time**](https://www.oliverburkeman.com/fourthousandweeks)?

We all might have a gut feeling about this, but what if we go ahead and extract data insights from our own calendar, to properly answer these questions?

Yes, I am proposing a data analytics project here, a very simple one, just to illustrate some concepts and some tools.

Using this sample project of calendar data, which is something we all can relate to, I want to introduce one of the main tools of the modern data stack: **dbt**, or data build tool. Let us find out what that is and how it can help us in our data analysis tasks and projects.

---

## Setting the stage: the data pipeline for our calendar project

We have data in a calendar (our source).

We currently use that data for _transactional_ purposes: we need that data to know which meeting to attend. When. Where. With whom. But also, to invite attendees. To reserve a meeting room. This is the natural use of that data.

What if we could also use this same data for supporting and improving our decision making, that is, for _analytical_ purposes? Well, we can! For seeing aggregates, extracting insights, answering those questions of how much we meet (yes, probably too much), predicting future behavior based on past data, even training some sort of AI model that will help us tackle that problem…

With this noble goal of data analysis in mind, we want to transport that data from its “natural” source, the calendar, through some “pipelines”, to expose it at some other end, in our case, a data report (from which we derive insights and analysis).

![Data pipeline diagram](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/blog/pipeline_diagram.png)

What is happening there?

We:
- **E**xtract data from its source.
- **L**oad it into an analytical database (e.g. a data warehouse),
- **T**ransform it to be easily used for analytics (e.g. a reporting tool such as Power BI, Tableau, Looker).

Enter the famous **ELT** in data operations.

(Incidentally, years ago, it used to be called ETL, but that is another topic).

Arbitrarily, for the rest of this article, we will focus on the **Transformation** stage, the **T**. Because that is what dbt does, and this is a post about dbt (in case it wasn’t clear yet).

Just remember that a complete data pipeline would include much more, and the modern data stack includes many fascinating processes, tools, technologies.

---

## Why do we actually need to transform our data?

Yes, why not just use it as it comes?

Because this is how data extracted from your calendar might look behind the scenes:

![Sample JSON data](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/blog/json_file.png)

This is a [JSON](https://www.json.org/json-en.html) object with meetings information. Typically, one JSON file would contain an array of objects with several meetings. Even if they are readable, it is hard to derive smart insights out of them, right away. For that, we might need to bring them together and transform them into more familiar _shapes_: tables of meetings, tables of assistants, tables of meeting categories, tables of locations, and so on. We might need to adjust the event dates and times for different time zones. We might need to join those tables together to make sense of the data. We might need to summarize or group some of them. And then we can start deriving the insights and analysis we want and we need.

Keep in mind that we are talking here about a relatively simple use case, calendar data. If we need to deal with data from more complex systems, like CRM, ERP, online stores, or anything like that, the case for data transformation is even stronger. I hope you get the idea.

Therefore, we need to move from Raw data to Transformed data, to facilitate our analysis:

![Raw to transformed data](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/blog/transformed_database.png)

**dbt** is THE tool that supports us in achieving these transformations.

---

## Using dbt to Transform our data

After extracting data from its source and loading it in our analytical database (in our case, the powerful [DuckDB & MotherDuck combo](https://motherduck.com/blog/dual-execution-dbt/)), we have raw data.

We now want to transform it into a structure that can be used for data analytics (reports, analysis, visualization).

To support us in these tasks, dbt provides a way to bring together:
- The most broadly available and well-known language for data querying and manipulation: SQL
- Jinja macros (wait, what? Yes, Jinja, it is just a way to include templates and macros into our SQL code… Ok, even simpler: let’s say supercharging SQL with extra powers)
- The ability to configure and run automated testing of our transformations
- An easy way to generate documentation
- Source control of our code (or the ability to track changes, collaborate with other developers, roll those changes back if someone messes up).
- A way to continuously integrate and deploy our Data analysis developments into Production systems.

If you have ever heard about software development operations (“DevOps”), what I just mentioned will sound familiar, but with a twist: DataOps.

In a nutshell, DataOps is bringing well-established practices of Software Development to Data Analytics: Source Control. Developers’ collaboration. Documentation. Testing. Different environments for development and production. Continuous Integration and Deployment between those environments, among others. In this way, we treat data analytics as what it really is: a software product well-deserving of all this systematic care.

dbt as a tool enables and facilitates DataOps for our data transformations.

---

## Understanding the transformation flow: lineage

Using dbt, what did we actually do to our data?

We took it from Raw.

We created some _staging_ models, which can be understood as intermediate models. In other words, they are the result of some initial transformations, but not yet clean enough to be consumed by our business users and analysts.

We then created _data marts_ out of those staging models. These data marts are now sufficiently transformed and can be consumed by business units interested in analyzing this data (in our simple project, I am the business unit interested in that analysis. But you get the idea).

These transformations can be visualized in what is called a data lineage:

![dbt lineage graph](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/blog/data_lineage.png)

As part of the documentation, dbt generates the lineage for us, together with a definition of the tables, their columns, the detailed SQL code used for transformations, and other additional, important information. Everything we need to continue expanding our development.

---

## Ok, and the final report?

We have transformed our raw data using dbt. We have exposed our _data product_ (that _data mart_) for someone to consume it. In our sample project, we use Power BI as the consumption tool for analysis. It connects to our Transformed database in MotherDuck and uses that information to generate a report.

Our first iteration of it looks like this:

![Power BI report screenshot](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/blog/power_bi_report.png)

Really? All this effort for just _this_?

Yes, but at least I can answer now: 1489 meetings in a year, an average of 124 meetings per month.

I grant you this: this was a very superficial data analysis. We want more. We need more. We can _now_ have more. We will ask someone to help us develop additional analysis based on that data…

And that is precisely what dbt **enables**. Collaboration. Easier development of data analysis. Bringing more people to the team. Having them easily understand what we did before, so that they can continue. Without spending a lot of time just deciphering what others did. Without losing the ability to roll back if they mess up in their new efforts.

So, this was just the beginning. Keep iterating, and you can get a report with _way_ more insights, more visuals, more analysis.

---

## Very few words on Tooling…

I don’t want to finish this post without mentioning the tools I used for this project, since tooling is a very important part of analytics engineering:

dbt-core. VS Code. DuckDB. MotherDuck. Git. GitHub. Power BI.

Forgive me for just dropping these names, without further explanation. For our purposes, it is enough to know that I spent _some time_ setting some of them up. Surely, there are [better, faster ways](https://datacoves.com/) to get you and your team started with professional-grade analytics engineering and data analytics.

As I mentioned before, what I described here doesn’t even cover a complete data pipeline. We missed tools for extraction, for loading, for orchestrating all the process. This was a tiny snapshot of a way larger and more fascinating process.

---

## Closing words

Our purpose here was to share some introductory ideas of what dbt is and how it can be used to transform data. We used a very simple data project, using calendar data, as an introduction to this tool as well as to some other basic concepts in the modern data stack and modern data operations.

If you made it until here, I’ll be bold and ask you for more of your precious time (yes, that time you saved by rejecting the invitation that just arrived for one particularly evil-looking meeting): Make sure to watch [this accompanying video](https://www.loom.com/share/24388e3dab5b4cc181d21fa2c95334c8) for more details about the data transformation process we performed in dbt.

I wouldn’t be posting this if dbt didn’t have the power to support us in more complex projects. It does. Get familiar with it.
