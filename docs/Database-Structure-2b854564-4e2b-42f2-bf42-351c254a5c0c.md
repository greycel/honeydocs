# Database Structure

## App Tables

These tables are all related to app-level settings such as the app theme and authentication. 

### Honey App

*User configurable: Yes*

*Parent Record: None*

The top level record for each Honey Application. An app is a collection of forms. Each app is assigned an App Theme and as a single entry form specified which is the default starting form. 

The default page for an app is generally the login page which does not require authentication. 

### Honey App Authentication Method

*User configurable: Yes*

*Parent Records: Honey App, Honey App Authentication Provider*

The App Authentication Method table holds records which specify how users can authenticate for the Honey App. Multiple authentication methods can be selected for a given app. There are currently four supported Authentication Providers for Honey Forms:

Authenticate with Google 

Authenticate with Microsoft 

Authenticate with Honey Forms Password

Authenticate with One Time Code

When authenticating with Google or Microsoft, additional configurations must be entered such as the Client ID (Google) or Tenant ID (Microsoft). These are also configured and stored on the Honey App Authentication Method page. 

### Honey App Authentication Provider

*User configurable: No*

*Parent Record: Honey App*

The list of authentication providers available for Honey Forms. These are part of the core app functions and not configured or added to by the user. 

### Honey App Access List

*User configurable: Yes*

*Parent Record: Honey App*

Access lists are created under each app. They specify which users are able to access pages in the app which require authentication. Access is always granted based on an email address. An access list record consists of a link to a saved search of any record type in NetSuite. The access list record also has a value which specifies the name of the email column on the saved search. 

### Honey User

*User configurable: No*

*Parent Record: None*

Honey User records are email addresses which have been setup to authenticate directly against a Honey password or a one-time code (OTC). Users do not need to authenticate using Honey passwords or via OTC. They can also authenticate using external authentication providers such as Google or Microsoft Auth. If the app uses an external authentication provider, there will be  no entries in the Honey User table. User Names are always unique email addresses.  

### Honey App User

*User configurable: No*

*Parent Record: Honey App*

The list of users which have logged into any of the Honey Apps. When a user logs in, a token and its expiration time is assigned and stored in this table. The token is passed via the URL from page to page once a users is authenticated and the user stays authenticated in the App until the token for that user has expired. The token is used by the app to determine which user is signed in when interacting with forms. Honey App User records are always created regardless of whether external authentication providers or built-in passwords or one-time codes (OTC) are used. 

### Honey Configs List

*User configurable: No*

*Parent Record: None*

This table contains a single record which stores app-wide configurations settings for the bundle. 

# Theme Tables

These tables are all concerned with the theme for the App which includes the look and feel and the specific page layouts which can be applied to each form. 

### Honey Theme

*User configurable: Yes*

*Parent Record: None*

A Honey Theme is set of base pages, styles, and layouts which can be used across the forms in an App. Pre-bundled themes exist and additional themes can be set up for specific Apps to customize the look and feel. A Honey Theme loosely corresponds to a Bootstrap Theme and indeed Bootstrap Themes which are available online can be converted into Honey Themes. 

Themes contain one or pages. Pages are template layouts into which the content of Honey Forms are embedded. The form theme pages used on individual forms can be set on the Honey Form record. 

### Honey Theme Web Asset

*User configurable: Yes*

*Parent Record: Honey Theme Page*

A Honey Theme Web Asset record associates a theme page with a required web-asset. The Theme Web Asset record can specify that the CSS or JavaScript asset is required on all theme pages or only specific pages. Web-assets which are required by both a theme and components on the page will only be rendered once. 

### Honey Theme Page

*User configurable: Yes*

*Parent Record: Honey Theme*

A Honey Theme Pages are single HTML page templates onto which Honey Form content can be rendered. The Theme Page forms the base for what is displayed to the user including the styling where components are placed on page. Honey Theme Page records always include a reference to a .html file stored in the file cabinet. 

The contents of the HTML pages include the full page content starting with the doctype tag. The pages must include: 

- A single Honey App div tag which all of the content is embedded within
- One or more section tags which are spaces on the page into which form components can be added.

The Honey App div tag is also used by the Vue.js framework as the main container for the app so all contents must reside inside this div tag. 

### Honey Theme Page Section

*User configurable: Yes*

*Parent Record: Honey Theme Page*

A theme page section is an area of a Honey Theme page into which form components can be added. Each theme page must have at least one page section but pages can have more than one. For example a page could have a section for the main content and a section for a sidebar. 

Page Sections are represented as a tag on the page within the actual Honey Theme Page HTML but must also be configured as a database record to indicate that form components can be added to that area. 

# Component Tables

These tables are all related to the re-usable components in the Honey Forms bundle. 

### Honey Component

*User configurable: Yes*

*Parent Records: Parent Honey Component (Optional), Honey Component Category*

A Honey Component is the main building block of the Honey Forms App. Components are pre-defined templates which can be added to pages and consist of a combination of HTML, CSS and JavaScript. Components can be re-used across multiple pages and can be either static layout-type components or data-driven components which bind to and allow data input and/or output from the NetSuite record connected to the specific form being viewed. 

Components can be directly added to Honey Forms or they can be "stacked" together to builder larger re-usable components which in turn can be added to Forms. An example might be a series of link components which are "stacked" into a custom side-bar component which is re-used on each form in a Honey App. 

### Honey Component Type

*User configurable: No*

*Parent Record: None*

A type field for components to indicate whether they they are either "Active" or "Static" type components. 

### Honey Component Category

*User configurable: No*

*Parent Record: None*

A grouping category for categorizing different components such as layout components and input field components. It does not drive functionality but merely provides a convenient way of organizing a long list of components available in Honey Forms. 

### Honey Component Setting

*User configurable: Yes*

*Parent Record: Honey Component, Honey Component Setting Type*

Each Honey Component is essentially a re-usable block of HTML, CSS styling and JavaScript code. When a component is initially designed and built, settings to be able to customize it can be defined as well. Each of these potential settings which can be configured are stored in the Honey Component Setting table. This table does not store the chosen settings for a given component when it is applied to a form but rather just the list of settings which are available to be selected for a given component and the options which can be applied for each setting. Generally when different data types are used, e.g. date versus text, entirely new components are configured rather than using Component Settings. Not all components require settings. 

Examples of settings couple be things like weather a field is read-only or mandatory, if a number field should allow decimals or not or the color of a button. Settings allow styling and layout variations on a single component without the need of setting up an entirely new component. 

### Honey Component Setting Type

*User configurable: No*

*Parent Record: None*

Indicates what type of value the setting requires for example a text value, a true/false value etc. 

### Honey Web Asset

*User configurable: Yes*

*Parent Record: Web Asset Type*

Honey Web Assets are any static assets such as CSS style sheets or JS libraries which are required by certain components. Each asset which is required by a component for it to function correctly is setup as a Honey Web Asset record and can then be added to the component as a required asset. When this is done, the Honey Forms bundle will automatically pick up on all assets required by the components being rendered on the form and include them on the page. Assets which are common to multiple components will only be rendered once using this scheme. 

When Honey Web Assets are set-up, the content can be added in one of three ways: 

- The content can be directly pasted into the Web Asset record
- The source document can be uploaded to the file cabinet and then referenced on the  Web Asset record.
- An external CDN hosted web-asset can be referenced by pasting in an HTML snippet on the Web Asset record which will be loaded in the page header when this asset is required on the page.

### Honey Web Asset Type

*User configurable: No*

*Parent Record: None*

This table stores the types which are referenced when setting up a Honey Web Asset and which determine how the asset should be rendered or served on the page. The currently available options are:

Style Sheet (.css)

Java Script (.js)

When a web-asset is setup it must be set-up for the correct type so that the Honey Forms bundle can serve the page with the correct content headers. 

### Honey Component Web Asset

*User configurable: Yes*

*Parent Record: Honey Component, Honey Web Asset*

This table records the instances of Web Assets which are required by Honey Components. This is the junction table which defines the requirement. When the Honey Forms bundle renders a form, it will look to this table to see which Web Assets need to be included on the page based on the components which are appearing on the page. 

### Honey Required Component

*User configurable: Yes*

*Parent Record: Honey Component, Honey Component*

An entry is made in the required component table whenever a component employs another component within its template definition. This Required Component record indicates to the Honey Forms bundle that the required component must be loaded onto the page for the form to render correctly. 

### Honey Data Type

*User configurable: No*

*Parent Record: None*

The data types are a list of NetSuite internal data types. The list is referenced in setting up data input components to indicate what type of fields they support a connection to. 

### Honey Dependent Component

(To be implemented)

### Honey Dependent Value

(To be implemented)

# Form Tables

These tables are all related to specific forms which are built out for a given app and the components which are added to those forms. 

### Honey Form

*User configurable: Yes*

*Parent Record: Honey App*

A Honey Form is a single location which a user can navigate to within a specific Honey App. Forms can be set to require authentication or to be publicly available. Forms consist of a series of components on the page which could components with static content, layout components or components which are bound to data sources in NetSuite. 

A form can be  configured to be associated with a specific record type to be able to read/write/create records of that type. When this is done, input field components can be added to the form and bound to specific fields on the NetSuite record type. These values will automatically load. 

Forms by default will render within the default theme page setup on the theme associated with the App, however, this can be set on the form level to override and use a different theme page within the same app theme. 

### Honey Sub-Form

*User configurable: Yes*

*Parent Record: Honey Form*

A Honey Sub-Form is used to render a different set of content within the same Honey Form. This can be used to break a form down into different sections or views which the user can navigate through without re-loading the whole page. 
Sub-forms are implemented using the Vue.js framework routes feature. A Honey Form loosely corresponds to a single page application in Vue.js and the Sub-Forms are the different views available. In Honey Forms, sub-forms must be associated with the same record type as the main form. It is just a way of separating which components are rendered at any given time as a user navigates to different sub-forms. 

### Honey Form Component

*User configurable: Yes*

*Parent Record: Honey Form, Honey Component*

Honey Form Components are instances of Honey Components being added to a form. When components are added to a form, the instance is stored in this table along with the sequence in which is should be rendered on the form and other custom configurations specific to this instance of the component being rendered. This configurations would include for example, which NetSuite input field the component is bound to, if any additional HTML classes are being applied to the component, which saved search drives the component data (in the case of a list component) etc. 

### Honey Form Component Setting

*User configurable: Yes*

*Parent Record: Honey Form Component*

Honey Form Component Settings are instances of Honey Component Settings  being configured for a specific form component. To clarify the pattern of how this works. Only settings which are pre-defined for the component can be set. 

Honey Component - the template component

Honey Component Setting - the list of available settings for the component

Honey Form Component - instance of the component on a form

Honey Form Component Setting - settings with chose values for the form component

### Honey Form Component Binding

*User configurable: No*

*Parent Record: None*

This table holds a short list of options of where active component values can be stored in the root data structure. 

### Honey Form Data Source

*User configurable: Yes*

*Parent Record: Honey App, Honey Form (optional)*

This record defines a data search based on a saved search which can be pre-loaded to forms for use in front end data manipulation. 

### Honey Form List Filter

(To be implemented)

### Honey Form Version

(To be implemented)

### Honey Record Data Type

*User configurable: No*

*Parent Record: None*

This table stores a list of possible data types which can be specified on a form. A given form is always connected to a single NetSuite record of a specified record type. For example a form might always be connected to Purchase Order records. The Record Data Type defines how the record is being interacted with. This data is important as the Honey Forms bundle needs to know how to retrieve the data from the database. The available options are:

Record - *values connected to the main record being viewed on the page*

Sub-List - *values are connected to a sub-list on the main record*

Read Only Search Rows - *values are an arbitrary list of search results related to the record*