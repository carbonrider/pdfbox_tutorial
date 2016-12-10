---
layout: home
title: Apache PDFBox Tutorial
comments: true
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Introduction
</div>

### Hello PDF World!

To begin with, let's create a Simple PDF with a single page that displays
**Hello World**.

Create a maven project and add the following block to dependencies section.

<pre>
<code class="html">
&lt;dependency&gt;
	&lt;groupId&gt;org.apache.pdfbox&lt;/groupId&gt;
	&lt;artifactId&gt;pdfbox&lt;/artifactId&gt;
	&lt;version&gt;2.0.3&lt;/version&gt;
&lt;/dependency&gt;
</code>
</pre>

Now under **src\main\java** create the package you desire, followed by a class
named as **HelloPDFWorld.java**. Refer below code snippet.

<pre>
<code class="java">
public class HelloPDFWorld {

	/**
	 * @param args
	 */
	public static void main(String[] args) throws Exception {
	}

}
</code>
</pre>

Once you are done with creating skeleton for the class. Add following block of
code to **main** method. Note that you should change the file path mentioned
in

<pre>
<code class="java">
PDDocument helloPdf = new PDDocument();
PDPage page = new PDPage(PDRectangle.A4);
helloPdf.addPage(page);

PDPageContentStream contentStream = new PDPageContentStream(helloPdf, page);
contentStream.beginText();
contentStream.setFont(PDType1Font.HELVETICA_BOLD, 10);
contentStream.newLineAtOffset(10, 100);
contentStream.showText("Hello PDF World!!!");
contentStream.endText();
contentStream.close();

helloPdf.save(new File("D:\\temp\\simple.pdf"));
helloPdf.close();
</code>
</pre>

Ensure there are no compilation error and run the main method. You should now
have a PDF created at the location specified while calling *save* method.

Lets just walkthrough the code, we have written. To create new PDF document,
PDFBox provides a class – *org.apache.pdfbox.pdmodel.PDDocument*.
You will find convenient methods like Saving PDF, adding signatures, adding new
pages etc. To create new document, just initialize it with empty constructor.

<pre>
<code class="java">
PDDocument helloPdf = new PDDocument();
</code>
</pre>

To add contents (text, image, form) in PDF, its necessary to create a page.
Additionally the page size must also be indicated using the static constants
available inside *org.apache.pdfbox.pdmodel.common.PDRectangle*
<pre>
<code class="java">
PDPage page = new PDPage(PDRectangle.A4);
helloPdf.addPage(page);
</code>
</pre>

*org.apache.pdfbox.pdmodel.PDPageContentStream* provides API to add text, images
etc. to the PDF page. Pass the *PDDocument* and *PDPage* reference to the constructor
of PDPageContentStream to get the instance. If you are using editor with AutoCompletion
feature, just type *contentStream.* and you should see several methods.
To start adding text, it is necessary to call *beginText* method on stream object.
Also setting a font is mandatory. PDFBox also provides option to embed custom fonts
to style the text as per the requirements. For the time being, lets just stick
to built-in font.
<pre>
<code class="java">
PDPageContentStream contentStream = new PDPageContentStream(helloPdf, page);
contentStream.beginText();
contentStream.setFont(PDType1Font.HELVETICA_BOLD, 10);
contentStream.newLineAtOffset(10, 100);
contentStream.showText("Hello PDF World!!!");
contentStream.endText();
contentStream.close();
</code>
</pre>

It is also necessary to specify the offset before adding text or by default text
will be added at the bottom of the page. Offset can be specified using *newLineAtOffset*
method, with two arguments - X and Y respectively. Note that Y offset is relative
to the bottom portion of the page. Try changing the values and re-run the code
to see the impact.
To add text at the specified offset, invoke *showText* method and pass *String*
argument. Invoke *endText* method to indicate, text addition is complete.
Finally, call *close* method on stream.

Finally, to save the document invoke *save* method on *PDDocument*, followed by
*close*.
<pre>
<code class="java">
helloPdf.save(new File("D:\\temp\\simple.pdf"));
helloPdf.close();
</code>
</pre>
