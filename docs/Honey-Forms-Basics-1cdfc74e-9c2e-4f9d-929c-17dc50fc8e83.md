# Honey Forms Basics

## Basic Concepts

The following are key concepts and definitions used in in the Honey Forms bundle and this documentation. Make sure to have a clear concept of these before continuing. 

## What is an App?

External forms built with Honey Forms are all contained within an App. Multiple Apps can be created for a single NetSuite Org but there must be at least one. 

The App which a form is created under determines the following:

- Who has access to the forms
- How users are meant to authenticate when reach the forms
- What the starting page or login page is for the app
- Each app has a unique URL
- The theme which determines the general look and feel of forms

An App will generally consist of a collection of several pages including a "login" page and a "main menu" type page where a user is directed once the log in. Before building an app it is wise to have a general design mapped out of the different pages and what the user will see on each page. 

## What are Components?

Components are elements which can be used in building forms such things as input boxes, text fields, date fields, lists, tables, etc. Components can be re-used several times on one form or on many different forms. There are a extensive set of basic components available upon install of the Honey Forms bundle but additional custom components can also be developed for specific use cases. Developing custom components is covered in the advanced topics. 

## What is a Form?

A Honey Form is a collection of components which are arranged on a page for the user to interact with. A form can be either externally visible without authentication (for example a leads capture web-form or a login page) or they can require authentication. 

Forms can display lists of information in to a user for example a dashboard which shows lists of recent Sales Orders and Invoices. Forms can also be linked to a specific record type, for example a Purchase Order so that when the form is submitted a new PO is created, or an existing PO is updated. 

Each form can only be linked to one record type and when being used for updates and record creates, one form is generally designed to update one record at a time. A general design pattern would be to have a "main page" with a table component showing a list of records and then a separate record form to be able to drill into a single record and make field changes and submit the form. This is a very similar patter to the way NetSuite works with lists showing multiple records and entry forms for editing single records.

When components are added to a form, it is specified what sequence they render in and what section of the form they appear in; such as the header, main body of the form or the footer. 

## What is a Form Component?

A Component, such as a text area field or a list, is a "template" which can be used on the form again and again. Components are setup in the system once and can be re-used in multiple places on multiple forms. Each time a component is added to a form, a "Form Component" record is created which records an instance of that component being used on the specified form. 

Form Component records point to the Form record and point to the Component record being used but they also contain a lot of additional configuration and settings information on how that component should be displayed on the form. Some examples of this are:

- The position of the component on the page
- The label of the component on the form
- If the component should be linked to a field in NetSuite
- Additional custom styles
- For table components, the saved search providing the data source

## What is a Theme?

A theme is a collection of base HTML pages and styles onto which different forms can be rendered. While the Form determines which interactive elements such as fields and buttons are displayed on the page, the Theme determines the overall style and structure of the page. 

A theme is applied at the App level and the same theme is used for all forms in the App. However, a Theme can contain different "Pages" which have different layouts and styles. One type of page might have a sidebar and header. Another page might be totally blank with just a content area.

Each form in an App will use the same Theme assigned at the App level but the different Forms can all be assigned different Theme Pages. 

## Full Honey Forms Records List

A full list of all records including additional technical details on the ones above can be found here [here](./Database-Structure-2b854564-4e2b-42f2-bf42-351c254a5c0c.md).