# Component Builder Values

**Important:** With the exception of the "c" values (see below), the tags can not be used in the Template HTML and JavaScript code blocks. They are designed only to be used used in the Instance HTML and JavaScript. They also can not be used in stacked components - only the top level component being rendered. "Active" components can access these same properties via the forms data structure. For more information see the [Building Honey Components](./Building-Honey-Components-1d1e380e-45bb-4ff6-8b17-565ca5f7854c.md) page.

## What are Component Builder Values?

Component builder values or just "builder values" are are used to embed values stored in the database into the component HTML and JavaScript. They make it possible to build more dynamic components which can be configured by users building forms. 

Components in Honey Forms consist of a combination of HTML and JavaScript code blocks as well as various settings and configurations which are stored in the database on the Component record. Builder values make it possible to embed these values into the HTML and JavaScript directly when writing components. 

## Referencing Builder Values

Builder values can be referenced in the JavaScript and HTML blocks using Builder Value Tags (described below). 

## Builder Value Tag Format

Builder values always consist of a prefix and a field name separated by a colon. When used in code blocks they are always opened and closed with a curly brace and a hash symbol. In general the format is as follows:

    {#prefix:fieldName#}

## Builder Value Types

For each of the types of builder values there is a specific prefix which is used to reference them in the HTML or JavaScript blocks of a component. The prefix is also closely related to the source table where the values are stored in the database. 

The following assumes an understanding of the relationships and differences between the Component, Form Component, Component Setting and Form Component Setting tables. 

**Component Values - Prefix "c"**

Component values are values which are stored on the Component table and are prefixed with a "c" when being used. These "c" values are available in both "instance" and "template" code blocks in components and can also be used in child components which are "stacked" into larger components. 

**Form Component Values - Prefix "fc"**

Form component values are values which are stored on the Form Component table and are prefixed with a "fc" when being used. 

These values can not be used in Template HTML/JavaScript code blocks. For more information see the [Building Honey Components](./Building-Honey-Components-1d1e380e-45bb-4ff6-8b17-565ca5f7854c.md) page.

**Component Setting Values - Prefix "cs"**

Component setting values are values which are stored on the Form Component Setting table and are prefixed with a "cs" when being used. If a component has settings defined which have not been assigned with a Form Component Setting record when the component was used on the form, then the default value on the Component Setting table will be used. 

There is no predefined list of "cs" builder values, they consist entirely of the settings which are made available for each component and are component specific. 

These values can not be used in Template HTML/JavaScript code blocks. For more information see the [Building Honey Components](./Building-Honey-Components-1d1e380e-45bb-4ff6-8b17-565ca5f7854c.md) page.

## Component Builder Values List

The following is a list of the supported builder values of the "c" and "fc" types. The underlying database field name which the values are taken from is also indicated. Unless otherwise stated, these builder values are available for use in both the HTML and JavaScript blocks. 

Many of these values are also available via the [Honey data structure](./Honey-Data-Structure-7992cfc5-8ba4-4fb8-a300-de79f8540a06.md) which is accessible via dynamic components once the page is rendered. Including the 

**c:template**

The value of the `hny_ct_common_html` field from the component table. This builder value is only available to be used in the JavaScript block and is specifically designed to be used to embed the HTML template into the Vue.js component definition in the JavaScript block. When this value is output it will be rendered with back-ticks surrounding the contents. An example of how it should be used is as follows. Note that no enclosing quotes are used as they will be added by the Honey Forms bundle. 

    Vue.component('component-test', {
    	template: {#c:template#}
    });

**fc:internalid**

 value of the `internalid` field of the form component which is being placed on the page. 

**fc:id**

This value should be used as the unique element ID value on the page for the component being rendered. Often a component will consist of several HTML elements. This should be used as the id attribute of the main element being rendered such as the id of an input field or data element. The ID should only be assigned to one single HTML element in the component as element IDs must be unique. 

**fc:name**

This is the value to be used on the name attribute of the element. If the component is being rendered as a sublist line, this value will also contain the sublist name and sublist line. The name will always contain the `hny_fc_source_field_id` value. 

**fc:label**

The value which is output for the component label will depend on the form component configurations.  If the `hny_fc_blank_label` field is set to true, the value will be empty. Otherwise the value of `hny_fc_label` on the Form Component record will be used. If no `hny_fc_label` is specified the standard `name` field of the Form Component will be used as the label. 

A simple example is as follows:

    <h2>{#fc:label#}</h2>

**fc:desc**

The display description to be rendered on the page. The value comes from the `hny_fc_display_description` field on the form component table. 

**fc:class**

Additional classes to be used in styling the element. Values are taken from the `hny_fc_additional_classes` field on the form component. This builder value should generally be added to the primary element in the component such as the input field. For example:

    <div class="form-group {#fc:groupClass#}">
        <label for="exampleEmail">Email address</label>
        <input type="email" class="form-control {#fc:class#}" >
    </div>

**fc:groupClass**

These classes should apply to the top level element in the template so that they are inherited by all containing elements. The above example shows correct usage of the `fc:groupClass` tag.

**fc:content**

This tag is used with a container type component which into which child form components can be placed and rendered. Grid rows and grid columns are examples of such components but more complex components can also be container components. 

Container components can be nested into a hierarchy with child components rendering on the page inside of other child components. This is common practice in creating dynamic, responsive bootstrap layouts. 

This tag like other "fc" tags can only be used in the instance HTML field so is generally not used with "active" honey components. For more information see [Building Honey Components](./Building-Honey-Components-1d1e380e-45bb-4ff6-8b17-565ca5f7854c.md).

An example of use of the `fc:content` tag is:

    <div class="row {#fc:class#}">{#fc:content#}</div>

**fc:authMethodClientId**

**fc:authMethodRedirectUrl**

**fc:authMethodTenantId**

**fc:sublistId**

**fc:sourceFieldId**

**fc:dataValue**

**fc:sourceSublistFieldId**

## Component Setting Builder Values

Component setting values are able to be referenced in the JavaScript or HTML blocks of a component by using the "cs" prefix and the developer/internal reference for the setting.

Component settings which are "text" type will simply render the text value wherever the builder value tag is used. True/False type settings will render either of the pre-defined true or false values depending on if the setting is set to true or false on the form component. 

An example of how a component setting type builder value could be used is as follows:

    <div class="form-group">
        <input type="text" isabled="{#fc:disabled#}" placeholder="{#fc:placeholder#}">
    </div>