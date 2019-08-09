# Component Definition File

Honey Components can be created and saved in a single component definition file and then very quickly updated in NetSuite on the Component record. 

## File Structure

The file format for a component definition file is as follows. The file is stored as a .html file and has several comment tags which define the different parts of the file. The comment tags are as follows:

- Honey Component {component tag name}
- Honey Component Instance HTML
- Honey Component Template HTML
- Honey Component Instance JavaScript
- Honey Component Template JavaScript
- Honey Component Template CSS

Example component definition file:

    <!--Honey Component sample-component -->
    
    
    <!--Honey Component Instance HTML -->
    <{#c:tagName#} :hny-fcid="{#fc:internalid#}" :hny="hny"></{#c:tagName#}>
    
    
    <!--Honey Component Template HTML -->
    <div class="form-group">
       <p>Some Sample Data</p>
    </div>
    
    
    <!--Honey Component Instance JavaScript -->
    <script></script>
    
    
    <!--Honey Component Template JavaScript -->
    <script>
    Vue.component('{#c:tagName#}', {
        props: ['hnyFcid', 'hny'],
        template: {#c:template#},
        data: function () {
            return {};
        }
    });
    
    
    <!--Honey Component Template CSS -->
    <style>
    .{#c:tagName#} input {
        font-weight: bold;
    }
    </style>

**Important Points:**

- The sequence of these tags in the file must be the same as shown above.
- The script tags for the JavaScript sections must be included
- The tag name must be included inside the first comment at the top of the page
- Additional whitespace does not matter inside or outside the comment tags

## Loading to NetSuite

The complete contents of the component definition file can be copied from the .html file and pasted directly into the "Component Definition" field on the Honey Component record. When this is done, each of the individual fields to store the Template HTML, Template JavaScript, Instance HTML and Instance JavaScript will be updated from the separate sections in the file. 

If an error occurs when the definition file is being parsed, the individual fields will not be updated and the "Component Definition" field will show the error after the record is saved.