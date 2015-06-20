# CloudWok file-upload embed widget

CloudWok is a Web service that enables you to receive uploaded files directly in a Dropbox folder, Google Drive folder, S3 bucket, Box.com folder, or Facebook photo album.

Learn how to embed a cloudwok widget into your own website. Thereby, you can create a form on your website where visitors of your website can upload files that are transferred directly into your connected Dropbox folder (or Google Drive folder, ...). It's easy. Trust me.

## File upload to your cloud

Add the CloudWok file-upload embed widget to your website to let visitors of your website upload files and receive the files in your favorite cloud storage: Dropbox, Google Drive, Amazon S3, Box.com, or Facebook.

<table>
    <tr>
        <td>
        ![file upload to Dropbox folder](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-dropbox.png "File upload widget for Dropbox")
        Let your website visitors upload files that are directly transferred to your Dropbox folder.
        </td>
        <td>
![file upload to Google Drive folder](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-google-drive.png "File upload widget for Google Drive")
Let your website visitors upload files that are directly transferred to your Google Drive folder.
        </td>
    </tr>
        <tr>
        <td>
![file upload to Amazon S3 bucket](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-aws-s3.png "File upload widget for AWS S3")
Let your website visitors upload files that are directly transferred to your Amazon We3b Services S3 bucket.
        </td>
        <td>
![file upload to Box.com folder](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-box.png "File upload widget for Box.com")
Let your website visitors upload files that are directly transferred to your Box.com folder.
        </td>
    </tr>
        <tr>
        <td>
![file upload to Microsoft OneDrive folder](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-microsoft-onedrive.png "File upload widget for Microsoft OneDrive")

... coming soon ...
        </td>
        <td>
![file upload to Facebook photo album](https://raw.githubusercontent.com/cloudwok/file-upload-embed/master/use-cases/images/cloudwok-embed-code-facebook-album.png "Photo upload widget for Facebook photo album")

Let your website visitors upload pictures, videos, and photos that are directly transferred to one of your Facebook albums. You can configure who can see the uploaded pictures by adjusting the privacy settings of your Facebook photo album (see "How Privacy Works for Photo Albums" https://www.facebook.com/help/385017548218624/).
        </td>
    </tr>
</table>

## Getting up-and-running in 5 minutes

1. Go to [https://www.cloudwok.com/](https://www.cloudwok.com/) and create an account.
2. Create a CloudWok that is either connected to a folder in your Dropbox, Google Drive, Box.com account or other cloud storage accounts that are supported by CloudWok.
3. After you have created a Wok, you get a URL to an upload website, such as this: https://www.cloudwok.com/u/ArK6. The last four digits are your "wok id" (in this example: ArK6).

## Examples

The following three examples show you how to integrate CloudWok into your website. The first approach is the easiest, just copy and paste the code into your website's HTML code where you need the widget.

The other two approaches (2 and 3) are a bit more advanced but give you more flexibility to customize the widget and integrate the CloudWok API deeper into your existing workflows.

### 1. copy & paste

... coming soon ...

### 2. blueimp/jQuery-File-Upload

Here is a [Demo](http://cloudwok.github.io/jQuery-File-Upload/) of jQuery-File-Upload with CloudWok back-end in action. The project's code is [here](https://github.com/cloudwok/jQuery-File-Upload). Only two minor changes of the orginal code by [blueimp](https://github.com/blueimp/jQuery-File-Upload) were necssary:

1. In the [index.html](https://github.com/cloudwok/jQuery-File-Upload/blob/master/index.html) file replace `<form id="fileupload" action="//jquery-file-upload.appspot.com/" method="POST" enctype="multipart/form-data">` with `html<form id="fileupload" action="https://www.cloudwok.com/api/rest/e/upload/YOUR_WOK_ID" method="POST" enctype="multipart/form-data">`. Replace `YOUR_WOK_ID` with your own wok id.
2. Remove (or comment out) the line `url: 'server/php/'` in [js/main.js](https://github.com/cloudwok/jQuery-File-Upload/blob/master/js/main.js)

That's it!

### 3. Your own file upload form

You can also build your own upload form if you don't want to use blueimp/jQuery-File-Upload. Here is [an example](https://github.com/cloudwok/embed/blob/master/examples/simple-upload-form.html) of how you might do this.

The upload form looks, for example, like this:

```html
    <form id="fileupload" method="POST" enctype="multipart/form-data">
      <input id="fileinput" type="file" name="files[]" multiple>
      <br />
      <br />
      <input type="submit" value="Upload now!" />
    </form>
```

You need to add some code to perform the upload. Here is an example with jQuery:

```javascript
var wok_id = "ENTER_YOUR_WOK_ID"
var cloudwok_upload_url = "https://www.cloudwok.com/api/rest/e/upload/" + wok_id;
$(function() {
  var data = new FormData();
  $.each(jQuery("#fileinput")[0].files, function(i, file) {
    data.append('file[]', file);
  });
  // POST request
  $.ajax({
    url: cloudwok_upload_url,
    data: data,
    cache: false,
    contentType: false,
    processData: false,
    type: 'POST',
  }).success(function() {
    $("#message").html("<a>File(s) uploaded. Yay!</a>");
  });
  return false;
  });
});

```

## Enforce file size and quota check

When you sign up for CloudWok, you get a free upload quota of 50MB per month and maximum file size of 5MB. If you have a paid plan, the allowed file size and quota limits are much higher. If you do not enforce a file size check and your CloudWok plan has no quota left (or files are too large), the file upload will not succeed. In such cases, you might want to inform your user, that the uploaded file was too large.

You can do so with the following code (requires jquery):

```html
<form id="fileupload" action="https://www.cloudwok.com/api/rest/e/upload/YOUR_WOK_ID" 
method="POST" enctype="multipart/form-data">
...
</form>
```
```javascript
<script>
     var wok_id = ENTER_YOUR_WOK_ID
     var jsonp_url = "https://www.cloudwok.com/api/rest/e/json/" + wok_id + "/details.json?callback=?";
      // retrieve quotas
      $.ajax({
        url: jsonp_url,
        dataType: "jsonp"
      }).then(function(resp) {
        availQuota = resp.availQuota;
        fileQuota = resp.fileQuota;
        // update the upload form
        $("#fileupload").attr("data-max-file-size", availQuota);
        $("#fileupload").attr("data-max-chunk-size", fileQuota);
      }, function(resp) {
        console.log("Whops. Cannot load widget, sorry. Is your wok-id correct?");
      });
</script>
```
