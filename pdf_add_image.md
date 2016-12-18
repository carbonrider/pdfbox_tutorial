---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: add_image
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Adding images
</div>

### Adding images

Apart from textual content, it is also possible to add images to PDF page. Apache
PDFBox offers convenient APIs to add images and offers supports for wide variety
of images including

- JPG / JPEG
- TIF / TIFF
- GIF / BMP / PNG

The most easiest way of adding image to PDF, is to use *PDImageXObject*. The class
offers methods *createFromFile*, *createFromFileByExtension*  and *createFromFileByContent*
etc., to get image instance either by file path or based on file extension or automatic
determination of the image type.

Refer following code snippet, which adds a .png image to PDF page.

<pre>
<code class="java">
public class EmbedImage {
    public static void main(String[] args) throws Exception{
        PDDocument pdDoc = new PDDocument();
        PDPage pdPage = addPage();
        pdDoc.addPage(pdPage);

        addImageToPage(pdDoc, pdPage);

        pdDoc.save("d:/temp/pdfWithImage.pdf");
        pdDoc.close();
    }

    private static PDPage addPage(){
        return new PDPage(PDRectangle.A4);
    }

    private static void addImageToPage(PDDocument pdDoc, PDPage pdPage) throws Exception{
        PDImageXObject pdImage = PDImageXObject.createFromFile("d:/temp/android.png", pdDoc);
        PDPageContentStream contentStream = new PDPageContentStream(pdDoc, pdPage);
        contentStream.drawImage(pdImage,10,400);
        contentStream.close();
    }
}
</code>
</pre>

Note the *addImageToPage* method, it constructs an instance of *PDImageXObject*
using *PDImageXObject.createFromFile* method, which accepts two arguments, file path
and an instance of *PDDocument*.

To add an image, using stream, have a look at the [PDImageXObject](https://apache.googlesource.com/pdfbox/+/trunk/pdfbox/src/main/java/org/apache/pdfbox/pdmodel/graphics/image/PDImageXObject.java)
source code. The code has lot of hints about using streams and offers convenient
API for determining file types. Additionally, the file provides hints about the
list of Image formats currently supported by Apache PDFBox.
