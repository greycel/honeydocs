# Honey Page Tags

## What are Honey Page Tags?

Honey Page Tags are used on Form Theme Pages to indicate where content should be added to the page. When a form is rendered the Honey Forms rendering engine will replace these tags with specific content configured for the App or Form. 

Page tags always take the form of an HTML comment so that if an admin user building forms adds a tag with a misspelled name, it will not appear to the end user on the screen or cause a hard error - it will simply render as an HTML comment rather than being replaced out. 

Users do not generally need to use these tags unless they are actually building a theme or making edits to an existing theme. Users who are building and editing forms as opposed to the form themes will not come into contact with these tags. 

## Honey Page Tag Format

Honey Page Tags always appear with two parts inside an HTML comment- the tag category and then the specific tag name separated by a colon. Examples of these tags are shown below. 

## Honey Page Tags List

These are the currently supported Honey Page Tags. Some of them are optional and some are required on all pages when creating a Form Theme Page. 

### HoneyForm:formTitle

*Required*

This tag is used to indicate where the form title will be rendered on the page. Here is an example of how this tag would be used on a page. 

    <head>
    	<title><!-- HoneyForm:formTitle --></title>

### HoneyForm:headContent

*Required*

The head content tag is replaced with all scripts and assets which are to be rendered in the head section of the HTML page. Web assets such as theme and component specific CSS would be examples of data which might be rendered in the place of this tag. 

The head content tag would be used in the following manner. 

    <head>
    	<meta charset="utf-8">
    	<!-- HoneyForm:headContent -->
    </head>

### HoneyForm:scriptsContent

*Required*

The scripts content tag is replaced with all JavaScript assets which are required by the theme or by specific components but which are not specifically configured to be loaded in the head content. 

The scripts content tag should be added within the body tags of the HTML page usually as one of the last items on the page. This generally sets up the best user experience when pages are being rendered. An example of the scripts content tag in use at the end of the page is as follows:

    		</div>
    	</div>
    
    	<!-- HoneyForm:scriptsContent -->
    
    </body>

### HoneyFormSection tags

Honey Form Section tags are used to indicate where content from form components is rendered on the page. Section tags are all named using the internal/developer name for the Theme Page Section. As a convention the main section of the page is usually named "content". 

Some pages only include a content section but page themes can also include sections for menus, headers, footers etc. The names of these sections including the main "content" will be listed on the Honey Theme Page record in NetSuite under the Page Sections sub-tab. 

The tag names used must correspond exactly to the internal/developer names for the sections listed in this sublist. 

An example of several content tags being used could be as follows:

    <div id="hny-app">
    
    	<div class="card">
    	    <div class="card-header">
    	      <!-- HoneyFormSection:headerContent -->
    	    </div>
    	    <div class="card-body">
    	      <!-- HoneyFormSection:content -->
    	    </div>
    	     <div class="card-footer">
    	     <!-- HoneyFormSection:footerContent -->
    	     </div>
    	  </div>
    	</div>