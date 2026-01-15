# How to add Google Analytics to a Harp boilerplate

This recipe shows you how to add Google Analytics to your Harp application in a configurable manner. This makes it easier for other people to make changes to the Google Analytics settings when digging into the templates.

## Adding Google Analytics

First, ensure you've actually created the site details in your Google Analytics account. You'll need to go to your *Property Settings* and find the *Tracking Id* value.

## Harp

### Using Jade

First, create a partial to include Google's embed code. 

_shared/analytics.jade

```jade
if service.analytics
  script.
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', '<#{ service.analytics }', 'auto');
  ga('send', 'pageview');
```

Then, set the values under the `globals` variable in _harp.json (or harp.json) file in the root of your project:

```json
"service": {
  "analytics": "UA-XXXX"
}
```

### Using EJS

First, create a partial to include Google's embed code. 

_shared/analytics.ejs

```ejs
<% if(service && service.analytics) { %>
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', '<%- service.analytics %>', 'auto');
  ga('send', 'pageview');

</script>
<% } %>
```
Then create the same _harp.json or harp.json described above.

