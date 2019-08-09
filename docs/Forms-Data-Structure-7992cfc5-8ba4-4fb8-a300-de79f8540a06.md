# Forms Data Structure

## Forms Data Structure

The "forms data structure" refers to the organization of data which is output to the browser page and which can be referenced and bound to by form components. Normal users will not need to interact directly with the forms data structure and even form administrators who are adding simple form components to forms will generally not need to work with it. 

The forms data structure becomes useful for developers who are building out more complex forms or who are directly authoring new Honey Components which can be re-used on forms. 

## Data Structure Map

The data structure can be viewed on any Honey form in the browser by looking at the `hny`  property attached to the browser window object. 

The data map is as follows:

    - hny
         - components
              - requiredComponents
         - data
              - documents
              - list
              - options
              - record
              - searchOptions
              - sublistOptions
              - sublists
              - form
              - var
         - form 
         - formComponents
              - [id] 
                    - settings
         - formComponentsIndex
         - formConfig
         - nav
         - params
         - redir
         - user

The primary values which are used in building custom Honey Components are described below. The `hny.data` values are very heavily used as all database records and search results which are loaded from NetSuite appear under this data object. 

## hny.data

The `hny.data` as mentioned above is an object which contains all of the dynamic search results, records and fields which are loaded from the database which the Honey Forms bundle is providing a means to interact with. Properties here can be directly bound to by components on the page. 

A list of the properties in the `hny.data` object are as follows:

**hny.data.record**

If the form being viewed is connected to a particular record type, this object comes into play. When an existing record such as a purchase order, a customer or any custom record for that matter is being viewed or edited on the screen, the `record` property will hold the field values for this record. Honey Forms is designed so that a given form can only edit one record at a time. That specific record being viewed on the screen and edited is stored in `hny.data.record` . 

When the data is submitted back to the server, it is taken from `hny.data.record` and posted back to be updated or inserted. 

**hny.data.form**

Any additional data which has not been loaded as part of the record from the page but has been created through fields on the form should be added under the `hny.data.form` object. Values which are collected on the form and need to be bound to a value but which are not part of the record loaded from NetSuite are stored here. This would included values like the user name and password fields for log-in components. 

## hny.formComponents

This property holds a list of all of the form components indexed by their internal ID numbers. A number of fields have been exposed for each form component.