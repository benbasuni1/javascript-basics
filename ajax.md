# AJAX
---
* Perform an asynchronous HTTP (Ajax) Request
* AJAX accepts 2 parameters : URL && SETTINGS  
    1. **URL** - A string containing the URL to which the request is sent.  
    2. **SETTINGS** - Options to configure AJAX request
* Default settings can bet set using $.ajaxSetup()

#### AJAX Setup
---
```js
// Ajax Init Setup
$.ajaxSetup({ SETTINGS })

// Regular Ajax Call
$.ajax({ URL, SETTINGS })
```
#### List of Settings
---
```js
const settings = 
{   
  // All ajax req are sent async, if sync is needed, set to false
  'async' : true,

  // Pre-req callback that can be used to modify jqXHR,
  // Use this to set custom headers
  'beforeSend' : function( xhr ) { },

  // If false, it will force req pages to not be cached by the browser
  // Using CodePen, this needs to be set to false
  'cache' : false,

  // Executes when Ajax call is finished [Regardless if successful or not]
  'complete' : function( xhr, textStatus ) { },

  'contents' : ,

  // Allow you to specify DOM element as context for (this) when complete/success 
  // is called.
  'context' : document.body,

  // This is the type of data I am sending to the server [ POST ]
  'contentType': 'application/json; charset=utf-8',

  // This is the type of data I am expecting back from the server
  'dataType' : 'json' || 'xml' || 'html' || 'text',

  // This function is called when a request fails
  'error' : function( xhr, textStatus, errorThrown ) {}

  // Send an object of additional header key/val pairs to be sent along with ajax call
  'headers': {
      "Accept"      : "text/plain; charset=utf-8",      
      "Content-Type": "text/plain; charset=utf-8"
  }
} 
```

