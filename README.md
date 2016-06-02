# Getting Started with DataBlade for Analysts

![screenshot](http://datablade.io/db-screen.png)

## Overview
Whether it's data from Google Analytics, Facebook, Salesforce, or your own internal SQL database, DataBlade enables you to instantly access your disparate sources and blend them seamlessly into intelligent reports that can be shared with your colleagues or run on an automated schedule.

*It's your data, in one central place, at your fingertips.*

## Adding Data Integrations
In order to access your data, you must first add your various sources as Data Integrations.

To add a Data Integration, click the **Data Integrations** button on the left and select the appropriate integration type from the dropdown.

![screen shot 2016-04-27 at 5 50 44 pm](https://cloud.githubusercontent.com/assets/1543187/14872382/a68b1c36-0ca0-11e6-8edc-da7480ac1e35.png)

Most integration types can be authenticated using a single click via OAuth. For certain integration types, you may have to provide additional information.

![screen shot 2016-04-27 at 5 54 53 pm](https://cloud.githubusercontent.com/assets/1543187/14872442/30578652-0ca1-11e6-83e5-befc25f691ad.png)

For all integrations, you will have to provide a **Name** value. Choose something that will help you remember what data is associated with the underlying source.

## Setting up SQL Integrations
In order to query data from your SQL database, you must ensure that it is properly configured to allow connections from our servers. In many cases, this is as simple as having your database administrator configure your database to accept connections from our IP address: `52.25.129.138/32`.

It is also generally advisible to have your DB administrator create a read-only account specifically for the DataBlade integration. 

If your database is behind a private network or if you need help setting up your connection, please contact us at support@datablade.io.

### SSL Certificates
If your database accepts encrypted connections, we recomend all users to set up their SQL integration with an SSL Root Certificate configured.

If you are using Amazon RDS, you can find the root certificate [here](https://s3.amazonaws.com/rds-downloads/rds-ca-2015-root.pem).

If you are using Amazon Redshift, you can find the root certificate [here](https://s3.amazonaws.com/redshift-downloads/redshift-ssl-ca-cert.pem).

## Creating a new Project

To create a new Project, click the **Projects** button on the left. Enter a name for your project at the field at the top of the page and click **Create Project**.

![screen shot 2016-04-27 at 5 58 13 pm](https://cloud.githubusercontent.com/assets/1543187/14872501/c578f98c-0ca1-11e6-95d0-c54bf3cf4a8d.png)

### Adding a Data Source to a Project

You can access your data in the Project interface by adding a data source.

![screen shot 2016-04-27 at 6 01 12 pm](https://cloud.githubusercontent.com/assets/1543187/14872527/131a7454-0ca2-11e6-9851-554821f8398c.png)

Each data source presents a query builder specifically designed to help you easily access data from that particular source.

![modules](https://cloud.githubusercontent.com/assets/1543187/14905222/890eaaa6-0d63-11e6-9b15-395ad6d414e9.png)

You can add multiple sources to bring in disparate data that is functionally related together into the same project.

Once you've set up your queries, hit the **Refresh Data** button at the top of the Project interface to fetch the data. You will see your results appear as tabs on the right side of the interface.

### Cleansing and Normalizing Data

All data source modules (except for those that are inherently SQL query driven) have a **SQL Filter** field. The purpose of this field is to allow you to treat the result set as if it were a dynamically generated temporary table, on which you can apply `SELECT` statements to clean, filter, and normalize the data.

For example, you can use the **Salesforce Query** module to do a very simple object query, and then use the SQL Filter to remove entries that do not meet a certain criteria:

![sqlfilter](https://cloud.githubusercontent.com/assets/1543187/14905383/e5b13b06-0d64-11e6-800d-5bb799ab80a4.png)

Since SQL Filters are always self-referential, in place of where you would put the table name, use `$self`. For example:

```sql
SELECT *
FROM $self
WHERE cast(AnnualRevenue as int) > 300000000
```

### Joining and Aggregating Multiple Sources

Once you have more than one data source module set up, you can now join and aggregate them into a single data set. From the Data Source dropdown, select **Utility (Join)**. Then, you can fill in the left and right join keys to define the join. As with all other data source modules, you can then use the **SQL Filter** functionality to additional grouping, filtering, and aggregation.

![join](https://cloud.githubusercontent.com/assets/1543187/14905625/48342552-0d67-11e6-80a1-32a76fe7132f.png)

### Excel Integration

The data displayed in the Project interface is a preview to help you define your queries and joins properly. Only 100 rows of each data set are displayed to you in the browser. In order to retrieve the entire data set, click the **Download Report to Excel** button in the top right.

Each data set will be placed onto its own sheet within the workbook.

#### Excel Templates

A common use case for Excel is to have multiple sheets containing different sets of data, then building a separate summary sheet that aggregates data across those different sheets. If you would like to include summary sheets in the Excel workbooks generated by DataBlade, you can use the Excel Template functionality.

Click the **Download Report to Excel** to download the initial, raw report. Then, you can use Excel to create any additional number of sheets that summarize that data. Once you have completed your template, click the down arrow next to the **Download Report to Excel** button and hit **Configure Excel Template**. Upload the workbook you just created.

All subsequent downloads of the Excel report for this project will be generated with your additional summary sheets included.

### Scheduling Jobs

In order to schedule your Project to be automatically run, hit the **Schedule** button in the top right. You will be prompted to define and schedule and list the emails you would like the output to be sent to. The resulting email will contain an attachment of the resulting Excel report. If you have an Excel template defined, it will generate using the template as a base.

## Support

Encountering problems or have general questions? Click the **Support** button on the left navigation and we'll get back to you as soon as possible.
