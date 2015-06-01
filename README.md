# CloudWok embed widget

CloudWok is a Web service that enables you to receive uploaded files directly in a Dropbox folder, Google Drive folder, S3 bucket, Box.com folder, or Facebook photo album.

Learn how to embed a cloudwok widget into your own website. Thereby, you can create a form on your website where visitors of your website can upload files that are transferred directly into your connected Dropbox folder (or Google Drive folder, ...). It's easy. Trust me.

1. Go to [https://www.cloudwok.com/](https://www.cloudwok.com/) and create an account.
2. Create a CloudWok that is either connected to a folder in your Dropbox, Google Drive, Box.com account or other cloud storage accounts that are supported by CloudWok.
3. After you have created a Wok, you get a URL to an upload website, such as this: https://www.cloudwok.com/u/ArK6. The last four digits are your "wok id" (in this example: ArK6).
4. Enter as your form's POST action: `https://www.cloudwok.com/api/rest/e/upload/ArK6` (replace ArK6 with your own wok id)

### Simple upload form



### jQuery-File-Upload

Here is a [Demo](http://cloudwok.github.io/jQuery-File-Upload/) of jQuery-File-Upload with CloudWok back-end in action. The project's code is [here](https://github.com/cloudwok/jQuery-File-Upload). Only two minor changes of the orginal code by [blueimp](https://github.com/blueimp/jQuery-File-Upload) were necssary:

1. In the [index.html](https://github.com/cloudwok/jQuery-File-Upload/blob/master/index.html) file replace `<form id="fileupload" action="//jquery-file-upload.appspot.com/" method="POST" enctype="multipart/form-data">` with `<form id="fileupload" action="https://www.cloudwok.com/api/rest/e/upload/YOUR_WOK_ID" method="POST" enctype="multipart/form-data">`. Replace `YOUR_WOK_ID` with your own wok id.
2. Remove (or comment out) the line `url: 'server/php/'` in [js/main.js](https://github.com/cloudwok/jQuery-File-Upload/blob/master/js/main.js)

That's it!
