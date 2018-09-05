# api2pdf.ckeditor4
CKEditor4 Plugin Code for [Api2Pdf REST API](https://www.api2pdf.com/documentation) 

Api2Pdf.com is a REST API for instantly generating PDF documents from HTML, URLs, Microsoft Office Documents (Word, Excel, PPT), and images. The API also supports merge / concatenation of two or more PDFs. Api2Pdf is a wrapper for popular libraries such as **wkhtmltopdf**, **Headless Chrome**, and **LibreOffice**.

This plugin adds a Save to PDF functionality to CKEditor4.  It will take the HTML contents of your editor, convert it to PDF, and request the web browser to download it.

The plugin will add an icon to the toolbar to Save to PDF.
![image](https://user-images.githubusercontent.com/7950956/45063742-9ca10900-b07d-11e8-928e-1b4754a4debf.png)

***
- [See Demo](https://www.api2pdf.com/ckeditor4-save-to-pdf-plugin/)
- [Get Started with CKEditor4 CDN](#ckeditor4-cdn)
- [Handlers and API Key](#handler)
- [PHP Handler](#php)
- [ASP.NET (.NET Core, MVC, Classic ASHX)](#aspnet)
- [FAQ](https://www.api2pdf.com/faq)


## <a name="ckeditor4-cdn"></a>Get Started with CKEditor4 CDN
This sample HTML initializes CKEditor4 via CDN and loads the latest Save-to-Pdf plugin via CDN.  This example HTML replaces all textareas in a document to use CKEditor4 loaded via CDN.  Take a look at the init method, to make use of the save to pdf plugin you should take note of the following steps:

1. Register save-to-pdf with addExternal
2. Register save-to-pdf in the extraPlugins section
3. Finally you must set the handler.  For more information on the handler [see this section](#handler)

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdn.ckeditor.com/4.10.0/standard/ckeditor.js"></script>
    <script>
        CKEDITOR.plugins.addExternal( 'save-to-pdf', 'https://rawgit.com/Api2Pdf/api2pdf.ckeditor4/master/plugins/save-to-pdf/', 'plugin.js' );
    </script>
</head>
<body>
    <textarea name="editor1"></textarea>
		<script>
			CKEDITOR.replace( 'editor1',
            {
                extraPlugins: 'save-to-pdf',
                pdfHandler: 'REPLACE-WITH-HANDLER-URL'
            } );
		</script>
</body>
</html>
```

## <a name="handler"></a>Handlers and API Key
Whether you are using the CDN or self-hosting, you will need a server side handler to process the PDF generation request.  This handler will take your incoming HTML and send it to Api2Pdf.com for processing.

1. Create an account at [portal.api2pdf.com](https://portal.api2pdf.com/register) to get your API key.
2. Use the approproiate code example for your platform of choice [PHP Handler](#php) or [ASP.NET](#aspnet)
3. Place your Api2Pdf API key in the handler code
4. Update the saveToPdfHandler configuration in your ckeditor replace function

## <a name="php"></a>PHP Handler and Sample Code
1. Download the PHP Source code here: https://github.com/Api2Pdf/api2pdf.ckeditor4/tree/master/handlers/php
api2pdf.php is the library code copied from https://github.com/Api2Pdf/api2pdf.php
index.html assumes the sample was copied to /php/savetopdf.php

2. In savetophp.php update the API key with the one you created at [api2pdf.com](https://portal.api2pdf.com/register)
```php
$a2p_client = new Api2PdfLibrary('YOURAPIKEY');
```

3. Update the saveToPdfHandler configuration in your ckeditor replace function. [See example](https://github.com/Api2Pdf/api2pdf.ckeditor4/blob/master/handlers/php/index.html)

## <a name="aspnet"></a>ASP.NET Handlers and Sample Code
1. The ASP.NET sample code makes use of the Nuget Package API2PDF.  Assuming you are building your own package you will first want to Install-Package Api2Pdf (https://github.com/Api2Pdf/api2pdf.dotnet)

2. Copy the appropriate handler code
- [.NET Core](https://github.com/Api2Pdf/api2pdf.ckeditor4/blob/master/handlers/DotNetExamples/AspNet.Core.Mvc/Controllers/SaveToPdfController.cs)
- [ASP.NET MVC](https://github.com/Api2Pdf/api2pdf.ckeditor4/blob/master/handlers/DotNetExamples/AspNet.Mvc/Controllers/SaveToPdfController.cs)
- [ASP.NET ASHX Handler](https://github.com/Api2Pdf/ckeditor4/blob/master/handlers/DotNetExamples/AspNet.WebForm/SaveToPdf.ashx.cs)

3. Regardless of which handler you copy, you will want to update this line of code with the API key you created at [api2pdf.com](https://portal.api2pdf.com/register)
```csharp
var a2pClient = new Api2Pdf("YOURAPIKEY");
```

4. Update the saveToPdfHandler configuration in your ckeditor replace function [See example](https://github.com/Api2Pdf/api2pdf.ckeditor4/blob/master/handlers/DotNetExamples/AspNet.WebForm/index.html)
