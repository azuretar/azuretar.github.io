---
id: 546
title: 'Azure Data Factory | Overview'
date: '2021-08-31T16:12:35+10:00'
author: 'Adriana Cavalcanti'
layout: post
guid: 'https://azuretar.com/?p=546'
permalink: /azure-data-factory-overview/
site-sidebar-layout:
    - default
site-content-layout:
    - content-boxed-container
theme-transparent-header-meta:
    - default
categories:
    - Azure
    - 'Data Factory'
---

Hiya there!

This is my first article here at AzureTar Blog and I am really excited to contribute with Data stuffs on Microsoft Azure! But let’s stop stalling and go straight to the point?

If you are familiar with SSIS (SQL Server Integration Services) or do not even know what that is but know at least do a Select query on SQL Server Management Studio (in short, SSMS), this article hopefully will not be hard to understand.

For completing its relational data service engine, Microsoft offers not only the well-known SQL Server, but also several services that help to manage different aspects of the way we manage, integrate, report and analyse data.

**SSMS (SQL Server Management Server):**  
This service is dedicated to managing and configuring any SQL infrastructure by running SQL queries, stored procedures and views on the databases.

**SSIS (SQL Server Integration Services):**  
This service is used to execute a wide range of migration tasks like data extraction, transformation (cleaning, aggregating, joining…) and loading. It basically moves relational data in different formats like Excel files, Oracle, DB2, and .csv into a SQL Server Database.

**SSRS (SQL Server Reporting Services):**  
This service allows us to create various interactive reports using graphs, maps, tabular reports, drill-down reports, click-through reports, and many more.

**SSAS (SQL Server Analysis Services):**   
It provides us with a great view of what is happening on our database using online analytical processing and data mining. In simple terms, we can use SSAS to create cubes using data from a data warehouse for deeper and faster data analysis.

To be fair, I have only used one of the four services and there was SSMS. I would load .txt files into a SQL Server table using BULK INSERT or an Excel file using OPENROWSET so then, after having the database clean and ready to be used, I would use either Excel or Tableau to create my reports and dashboards.

As we can see, Microsoft offers us softwares and solutions for each step in our data process. Not too different from on-premise, MS also helps us with a bunch of cloud-based alternatives and this platform is known as **<span class="has-inline-color" style="color:#0270a0">Azure</span>**.

> The Azure cloud platform is more than 200 products and cloud services designed to help you bring new solutions to life – to solve today’s challenges and create the future. Build, run and manage applications across multiple clouds, on-premises and at the edge, with the tools and frameworks of your choice.
> 
> <cite>Microsoft Azure</cite>

<div class="wp-block-group alignwide"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">---

# Azure Data Factory

In this article, we are going to talk about the **Data Factory Platform** which is the cloud-based alternative for **SSIS**.

</div></div><div class="wp-block-image"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/08/ADF-SSIS-1200x677.png)</figure></div><div class="wp-block-media-text is-stacked-on-mobile is-vertically-aligned-center" style="grid-template-columns:35% auto"><figure class="wp-block-media-text__media">![](https://azuretar.com/wp-content/uploads/2021/08/AzureLogo-e1630384337352.png)</figure><div class="wp-block-media-text__content">> Cloud-based data integration services orchestrate and automate data movement and data transformation.

If you did not understand what that means, no worries. I am still not getting it as well. If it helps I prefer the definition:  
Data Integration Service: Gathers data from multiple sources and provides a consolidated outcome of them.

</div></div>Basically, for those who are coming from SSIS or have played with SQL Queries before, Azure Data Factory is all about **extraction**, **manipulation** and **saving** the data. It is the first step to be taken when we initiate our journey in data workload. Unless we already have everything set into our Database, which is unlikely to happen in real life. The terms that define better what ADF performs are more known as **E**xtraction-**T**ransformation-**L**oad (the famous ETL).

<div class="wp-block-group alignwide"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">---

## What is ETL?

In data engineering, the most data integration pattern is ETL (there is a pattern known as ELT which basically is in a different order of ETL process).

</div></div><div class="wp-block-columns is-layout-flex wp-container-core-columns-is-layout-3 wp-block-columns-is-layout-flex"><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow"><div class="wp-block-image"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/08/Extration.png)<figcaption>**EXTRACTION**</figcaption></figure></div>Where the datasets are coming from

It is called **Data Source** the resource that we link the servers where our data is coming from. Here we use something similar to connection strings. In other words, we will connect to the sources to be able to collect them.

</div><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow"><div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2021/08/transformation.png)<figcaption>**TRANSFORMATION**</figcaption></figure></div>What we want to change

Performs on the data transforming and enriching it. Here we **manipulate** and **change** the data using processes such as aggregations, cleansing, filtering, joining, summarization and so on.

</div><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow"><div class="wp-block-image"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/08/load-1200x1200.png)<figcaption>**LOAD**</figcaption></figure></div>Where we want to store

Once we get the data modified, we can store it into a destination called **Sink** such as [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#mapping-data-flow-properties) or [Azure SQL Database](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-database#mapping-data-flow-properties). We need to have at least one sink transformation for every data flow due to the fact that ADF does not store any data.

</div></div>Putting it in an example, let’s imagine we work for a video streaming company and they want us to inspect some marketing analysis: customer behaviors, customer demographics and their preferences in terms of movies. We have petabytes of video logs data in the cloud, customer reviews on Hadoop and their latest watched movies on MongoDB.

We can just export the files from their sources and upload them into SQL Server Database and do the job there. However, it would take us forever to export, load and transform the data. Big data needs a scalable service that can ORCHESTRATE the data movement and AUTOMATE the data transformation. In our case, we have raw and unorganized data relational and non-relational coming from different storage systems. So that is where the ADF comes in to show us its power!

At a high level of collecting from sources, processing to transform, publishing into a warehouse for analysts, and monitoring and managing daily schedules, Azure is a set of interconnected systems and gives us an end-to-end platform for our data engineering.

<div class="wp-block-group alignwide"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">---

## What Else About ADF?

Okay! That ADF helps us with Data Integration at cloud scale, we already know, but what we do not know yet is that on ADF we also can

</div></div><div class="wp-block-columns is-layout-flex wp-container-core-columns-is-layout-4 wp-block-columns-is-layout-flex"><div class="wp-block-column is-vertically-aligned-top is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:25%"></div><div class="wp-block-column is-vertically-aligned-center is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:50%">- DRAG AND DROP: ADF is code-free transformation;
- CAN CODE (if you prefer): ADF runs code on any Azure Compute;
- USE SSIS PACKAGES: Many SSIS Packages run on Azure;
- DATA OPS on GITHUB ou AZURE DEVOPS: Source control automated deploy for DataOps;
- SECURE our DATA: Secure data integration by connecting to private endpoints that are supported by various Azure data stores.

</div><div class="wp-block-column is-vertically-aligned-top is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:25%"></div></div><div class="wp-block-group alignwide"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">---

## Key Concepts

ADF has 6 main components to do its hybrid data integration at enterprise scale easy and they are:

</div></div><div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow"><div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow"><div class="wp-block-columns is-layout-flex wp-container-core-columns-is-layout-5 wp-block-columns-is-layout-flex"><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:33.34%"></div><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:65%">- **Pipelines**: Group of all activities needed to perform one unit of work.
- **Activities**: Each step performed on the data (copy, move, transform, enrich, etc.).
- **Integration Runtimes:** Computing Infrastructure of the ADF (Azure Integration Runtime and Self-Hosted Runtime).
- **Triggers**: When everything starts it is like a power switcher.
- **Datasets**: Files or SQL tables.
- **Linked Servers**: Offers more than 90 connectors.

</div><div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:33.33%"></div></div></div></div>If you forget about any concept above. That’s okay. We will cover each one along with this series either publishing more on AzureTar Blog and/or through recorded hands-on videos. This was just a short introduction to ADF. What it offers and how it does.

Do not miss out, follow us and stay tuned!

</div></div><div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow"><div class="wp-block-image is-style-rounded"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2020/10/profile.png)<figcaption><span class="has-inline-color" style="color:#11415e">Adriana Cavalcanti  
</span>*Data Engineer*</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.23,5.924c-0.736,0.326-1.527,0.547-2.357,0.646c0.847-0.508,1.498-1.312,1.804-2.27 c-0.793,0.47-1.671,0.812-2.606,0.996C18.324,4.498,17.257,4,16.077,4c-2.266,0-4.103,1.837-4.103,4.103 c0,0.322,0.036,0.635,0.106,0.935C8.67,8.867,5.647,7.234,3.623,4.751C3.27,5.357,3.067,6.062,3.067,6.814 c0,1.424,0.724,2.679,1.825,3.415c-0.673-0.021-1.305-0.206-1.859-0.513c0,0.017,0,0.034,0,0.052c0,1.988,1.414,3.647,3.292,4.023 c-0.344,0.094-0.707,0.144-1.081,0.144c-0.264,0-0.521-0.026-0.772-0.074c0.522,1.63,2.038,2.816,3.833,2.85 c-1.404,1.1-3.174,1.756-5.096,1.756c-0.331,0-0.658-0.019-0.979-0.057c1.816,1.164,3.973,1.843,6.29,1.843 c7.547,0,11.675-6.252,11.675-11.675c0-0.178-0.004-0.355-0.012-0.531C20.985,7.47,21.68,6.747,22.23,5.924z"></path></svg><span class="wp-block-social-link-label screen-reader-text">Twitter</span>](https://twitter.com/driicavalcanti)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/drii-cavalcanti/)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M12,2C6.477,2,2,6.477,2,12c0,4.419,2.865,8.166,6.839,9.489c0.5,0.09,0.682-0.218,0.682-0.484 c0-0.236-0.009-0.866-0.014-1.699c-2.782,0.602-3.369-1.34-3.369-1.34c-0.455-1.157-1.11-1.465-1.11-1.465 c-0.909-0.62,0.069-0.608,0.069-0.608c1.004,0.071,1.532,1.03,1.532,1.03c0.891,1.529,2.341,1.089,2.91,0.833 c0.091-0.647,0.349-1.086,0.635-1.337c-2.22-0.251-4.555-1.111-4.555-4.943c0-1.091,0.39-1.984,1.03-2.682 C6.546,8.54,6.202,7.524,6.746,6.148c0,0,0.84-0.269,2.75,1.025C10.295,6.95,11.15,6.84,12,6.836 c0.85,0.004,1.705,0.114,2.504,0.336c1.909-1.294,2.748-1.025,2.748-1.025c0.546,1.376,0.202,2.394,0.1,2.646 c0.64,0.699,1.026,1.591,1.026,2.682c0,3.841-2.337,4.687-4.565,4.935c0.359,0.307,0.679,0.917,0.679,1.852 c0,1.335-0.012,2.415-0.012,2.741c0,0.269,0.18,0.579,0.688,0.481C19.138,20.161,22,16.416,22,12C22,6.477,17.523,2,12,2z"></path></svg><span class="wp-block-social-link-label screen-reader-text">GitHub</span>](https://github.com/drii-cavalcanti)

Sources:  
 – <https://docs.microsoft.com/en-us/azure/data-factory/introduction>  
 – <https://adf.azure.com/datafactories>

</div></div>