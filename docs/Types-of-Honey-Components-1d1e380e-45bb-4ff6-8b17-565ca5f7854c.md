# Types of Honey Components

## Static vs. Active Components

There are two general approaches to creating Honey Components. Components can either be "static" or "active".  Here are the basic definitions of each. Further details on how to setup static and active components follows further below.

**Static Components**

Static components simply render pre-defined HTML to the page. The component values are pre-processed server-side before the page is rendered and the resulting elements are rendered to the screen.

Static components work best for form layout or design structures which do not contain any dynamic or data-driven content or which contain read-only data which is output on the form but does not get edited by the user. Static components can include simple JavaScript which performs scripted actions on the page but generally this is better accomplished with Active components. 

**Active Components**

Active components are defined as an HTML template using the Vue.js framework. The template JavaScript and HTML are rendered on the page and then the data values are rendered on the page within the component markup by the Vue.js framework in real-time after the page is loaded. 

Active components need to be used whenever input fields are used or where data is edited by the user and sent back to NetSuite. Active components are also better suited to building interactive elements on the screen which change or respond to user input. 

## Common vs. Instance Code Blocks

The HTML and JavaScript blocks are the primary ingredients in a Honey component. When setting up a component there are fields to add "Common" and "Instance" JavaScript and HTML. 

Common code is output on the page once no matter how many times the component is used on the page and must be written in a general fashion to apply or be re-used no matter how many times the component is used on a page. 

Instance code is rendered each time the component is used on the page. 

## Container Components

## Stacked Components

## Honey Components Rendering Sequence

When the Honey Forms bundle renders components to the screen it takes the following steps server side before the components are output to the screen as part of the form:

- Check which components are used on the current form being viewed
- Load the underlying components from the Components table including the component HTML and JavaScript
- Load the configurations for how they are used on the form from the Form Components table
- Load all of the applicable settings from the Component Settings table
- Applies the component settings values where they are referenced in the HTML and JavaScript blocks
- Loads the record data and saved search data which is used by the components
- Renders the components as part of the form in the browser
- Outputs the related record data and saved search data to the browser
- Active components then execute on the page after page load pulling in any data values as required.