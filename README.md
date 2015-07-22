# CloudWok file-upload embed widget

CloudWok is a Web service that enables you to receive uploaded files directly in a Dropbox folder, Google Drive folder, S3 bucket, Box.com folder, or Facebook photo album.

Learn how to embed a cloudwok widget into your own website. Thereby, you can create a form on your website where visitors of your website can upload files that are transferred directly into your connected Dropbox folder (or Google Drive folder, ...).

Take a look at the [wiki](https://github.com/cloudwok/file-upload-embed/wiki) for further information.

If you have any questions or issues, you can also reach out to us on [StackOverflow](http://stackoverflow.com/questions/tagged/cloudwok) - just tag your question with "cloudwok".

## Demo

[Demo of simple file-upload widget](https://cloudwok.github.io/file-upload-embed/)

![CloudWok Embed Code Demo](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-widget-demo-website-screenshot.png "CloudWok Embed Code Demo")

## Get up-and-running in 3 minutes

1. Go to [https://www.cloudwok.com/](https://www.cloudwok.com/) and create an account.
2. Create a CloudWok that is either connected to a folder in your Dropbox, Google Drive, Box.com account or other cloud storage accounts that are supported by CloudWok.
3. After you have created a Wok, you get a URL to an upload website, such as this: https://www.cloudwok.com/u/AneJ. The last four letters are your "wok id" (in this example: AneJ).

## Examples

The following example shows you how to integrate CloudWok into your website. The copy & paste approach is the easiest, just copy and paste the code into your website's HTML code where you need the widget.

Other approaches are explained in the [wiki](https://github.com/cloudwok/file-upload-embed/wiki) and are a bit more advanced but give you more flexibility to customize the widget and integrate the CloudWok API deeper into your existing workflows.

### Copy & paste widget code into your website

Here is [a simple example](https://github.com/cloudwok/file-upload-embed/blob/gh-pages/index.html) which shows you how you can add the file-upload widget to your website.

The file-upload embed widget has two parts. First the HTML part:

```html
<div class="cloudwok-embed" data-wokid="ENTER_YOUR_WOK_ID">
  <div class="cloudwok-upload-files"></div>
  <form class="cloudwok-upload">
    <div class="cloudwok-dropzone"></div>
  </form>
  <div class="cloudwok-download-files"></div>
  <div class="cloudwok-upload-message"></div>
</div>
```

In the HTML code, you must replace the placeholder `ENTER_YOUR_WOK_ID` with the wok id of your own wok.

You must also add the following JavaScript code to your website. You can paste the JavScript code at the bottom of your page (just over the closing `</body>` tag) to make your page load faster. (The page will not really load faster, but the visible content will be shown earlier to the user which makes is appear as if the page loads faster).

```javascript
<script>
  (function(window, document) {
    var loader = function() {
      var script = document.createElement("script"),
      tag = document.getElementsByTagName("script")[0];
      script.src = "https://www.cloudwok.com/cdn-vassets/javascripts/cw.js";
      tag.parentNode.insertBefore(script, tag);
    };
    window.addEventListener ? window.addEventListener("load", loader, false) :
    window.attachEvent("onload", loader);
  })(window, document);
</script>
```

You can decide which features you would like to add to your website:

| JavaScript                |  Feature                  |
|---------------------------|---------------------------|
| `<div class="cloudwok-upload-files"></div>` | Show files that an uploader uploaded to the uploader |
| ```javascript<div class="cloudwok-dropzone"></div>``` | Show the dropzone where files can be dragged & dropped or added to initiate a file upload |
| ```javascript
<div class="cloudwok-download-files"></div>
```  | Show all files that have been uploaded by all uploaders |
| ```javascript
<div class="cloudwok-upload-message"></div>
```  | Show a message form that enables the uploader to send a message to the receiver of the file, i.e., to the cloudwok owner |

If you add the `<div class="cloudwok-upload-message"></div>`, a simple message form field is shown that allows your uploaders to send a message along with the uploaded file(s). You can add e-mail and first-name / last-name fields to the message form by adding the following attributes:

```html
<div class="cloudwok-embed" data-show-name="y" data-show-email="y" data-wokid="YOUR_WOK_ID">
...
</div>
```

You would like to send the download-links (links to the files which are uploaded) with a different form or method directly to your own system, not with our upload form? You can do that! You can further customize the widget by specifying a jQuery selector that pastes the download-links as blank-separated list into an HTML element of your choice via `data-uploaded-files-target-selector`:

```html
<div class="cloudwok-embed" data-uploaded-files-target-selector="..." data-wokid="YOUR_WOK_ID">
...
</div>
```

More info coming soon...

### WordPress plugin

You can add the CloudWok [Wordpress plugin](https://github.com/cloudwok/file-upload-wordpress-plugin) to your WordPress blog or website.

1. Search for the CloudWok plugin in the WordPress Plugin Directory (left-hand sidebar in your WordPress admin dashboard): [https://wordpress.org/plugins/cloudwok-file-upload/](https://wordpress.org/plugins/cloudwok-file-upload/)
2. Activate the plugin.
3. Add shortcodes to your page like this:

`[cloudwok wok_id="YOUR_WOK_ID" show_uploads="False" show_downloads="True" show_form="True"]`
