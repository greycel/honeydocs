# Building Static Components

## Building Custom Static Components

When writing static components the code blocks are used as follows. An example is given of a sub-heading component which renders the label as specified on the form component. For illustrative purposes this component has some JavaScript which adds the current date under the heading. 

**Template HTML**

Not used.

**Instance HTML**

The component HTML elements are entered here along with any [Builder Value Tags](https://www.notion.so/Honey-Component-Builder-Values-888b2919953841e1b470f1f72885a7ab) to add database values to the component when they are rendered on the page. Example:

    <div>
    	  <h2>{#fc:label}</h2>
        <span id="date_span_{#fc:internald#}"></span>
    </div>

**Template JavaScript**

Helper functions which need to be added to the page to allow this component to correctly function are added here. Functions names should generally be name-spaced or prefixed in order to prevent conflicts between components but this is left to the discretion of the user. Any JavaScript added in this section will only ever be written once to the page as long as the component is used at least one time on the page. The Template JavaScript is not "aware" of the form component instance being used and Builder Value Tags can not be used in the Template JavaScript. 

    var dh = dh || {};
    dh.setDateheaderDate = function(formComponentId) {
    	  var theDate = new Date();
        var dtElementId = 'date_span_' + formComponentId;
    	  document.getElementById(dtElementId).innerHTML = theDate.toLocaleDateString();
    }

**Instance JavaScript**

Instance JavaScript is rendered on the page again each time the component is used on the page. Instance JavaScript should generally be kept short with the main logic handled by Template JavaScript functions. 

    dh.setDateheaderDate('{fc:internalid}');