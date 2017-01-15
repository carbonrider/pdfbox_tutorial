---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: new_pdf_form
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Simple Form
</div>

### Simple Form

PDF form is a great option to distribute and accept data from users, without a need
to host a website. PDF form is similar to Paper form, but in digital form. The wide
variety of options makes it perfect choice of tool to capture data.

Apache PDFBox provides low level APIs to create PDF forms with rich set of controls
and to specify rich formatting options.

To begin with, create a new document and add a A4 sized page to it.

<pre>
<code class="java">
PDDocument pdDocument = new PDDocument();
PDPage page = new PDPage(PDRectangle.A4);
pdDocument.addPage(page);
</code>
</pre>

Next create an AcroForm, using *PDAcroForm* API and add it to the page. Note, you
can only set one AcroForm instance per PDF.

<pre>
<code class="java">
PDAcroForm form = new PDAcroForm(pdDocument);
pdDocument.getDocumentCatalog().setAcroForm(form);
</code>
</pre>

Setting default resources for the form is mandatory and it can be done using
following code

<pre>
<code class="java">
PDFont font = PDType1Font.HELVETICA;
PDResources resources = new PDResources();
resources.put(COSName.getPDFName("Helv"), font);
form.setDefaultResources(resources);
</code>
</pre>

It is possible to specify different or multiple fonts for PDF form. If default
resources are not specified, following exception will be generated.

<pre>
<code class="plain">
Exception in thread "main" java.lang.IllegalArgumentException: /DR is a required entry
</code>
</pre>

Its time to add Text Field to the form. PDFBox provides *PDTextField* API to add
text field which can accept input from user and its contents can be saved along
with PDF.

<pre>
<code class="java">
PDTextField textField = new PDTextField(form);
textField.setPartialName("SampleField");
</code>
</pre>

Similar to setting default resources, form field must also have default appearance
settings.

<pre>
<code class="java">
String defaultAppearance = "/Helv 12 Tf 0 0 1 rg";
textField.setDefaultAppearance(defaultAppearance);
</code>
</pre>

If the default appearance of the field is not set, PDFBox will thro an exception.
The arguments specify, font name, size, color to be used for the given field.
If you wish to auto resize the field font based on the content, change the font
size value from 12 to 0. This will lead to fit the text within the visible area
of the field.

Add the text field to form

<pre>
<code class="java">
form.getFields().add(textField);
</code>
</pre>

To specify the location of field, PDFBox offers *PDAnnotationWidget*.

<pre>
<code class="java">
PDAnnotationWidget widget = textField.getWidgets().get(0);
PDRectangle rect = new PDRectangle(50, 750, 200, 50);
widget.setRectangle(rect);
widget.setPage(page);
</code>
</pre>

Use *PDRectangle* to specify, x & y location, followed by width, height of the
textfield.

Next step is to specify, display settings for the field and it is completely optional.
Below code sets border and background color using RGB color.

<pre>
<code class="java">
PDAppearanceCharacteristicsDictionary fieldAppearance = new PDAppearanceCharacteristicsDictionary(new COSDictionary());
fieldAppearance.setBorderColour(new PDColor(new float[]{0,1,0}, PDDeviceRGB.INSTANCE));
fieldAppearance.setBackground(new PDColor(new float[]{1,1,0}, PDDeviceRGB.INSTANCE));
widget.setAppearanceCharacteristics(fieldAppearance);
</code>
</pre>

Finally, the widget instance must be added to the page and field can be initialized
with default value.

<pre>
<code class="java">
widget.setPrinted(true);
page.getAnnotations().add(widget);
textField.setValue("Sample Field");

//Save the PDF to a location.
pdDocument.save("d:/temp/sample_form.pdf");
pdDocument.close();
</code>
</pre>

All of this together.

<pre>
<code class="java">
import org.apache.pdfbox.cos.COSDictionary;
import org.apache.pdfbox.cos.COSName;
import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.pdmodel.PDPage;
import org.apache.pdfbox.pdmodel.PDResources;
import org.apache.pdfbox.pdmodel.common.PDRectangle;
import org.apache.pdfbox.pdmodel.font.PDFont;
import org.apache.pdfbox.pdmodel.font.PDType1Font;
import org.apache.pdfbox.pdmodel.graphics.color.PDColor;
import org.apache.pdfbox.pdmodel.graphics.color.PDDeviceRGB;
import org.apache.pdfbox.pdmodel.interactive.annotation.PDAnnotationWidget;
import org.apache.pdfbox.pdmodel.interactive.annotation.PDAppearanceCharacteristicsDictionary;
import org.apache.pdfbox.pdmodel.interactive.form.PDAcroForm;
import org.apache.pdfbox.pdmodel.interactive.form.PDTextField;

public class NewForm {

    public static void main(String[] args) throws Exception{
        PDDocument pdDocument = new PDDocument();
        PDPage page = new PDPage(PDRectangle.A4);
        pdDocument.addPage(page);

        PDAcroForm form = new PDAcroForm(pdDocument);
        pdDocument.getDocumentCatalog().setAcroForm(form);

        PDFont font = PDType1Font.HELVETICA;
        PDResources resources = new PDResources();
        resources.put(COSName.getPDFName("Helv"), font);
        form.setDefaultResources(resources);

        PDTextField textField = new PDTextField(form);
        textField.setPartialName("SampleField");

        String defaultAppearance = "/Helv 12 Tf 0 0 1 rg";
        textField.setDefaultAppearance(defaultAppearance);

        form.getFields().add(textField);

        PDAnnotationWidget widget = textField.getWidgets().get(0);
        PDRectangle rect = new PDRectangle(50, 750, 200, 50);
        widget.setRectangle(rect);
        widget.setPage(page);

        PDAppearanceCharacteristicsDictionary fieldAppearance = new PDAppearanceCharacteristicsDictionary(new COSDictionary());
        fieldAppearance.setBorderColour(new PDColor(new float[]{0,1,0}, PDDeviceRGB.INSTANCE));
        fieldAppearance.setBackground(new PDColor(new float[]{1,1,0}, PDDeviceRGB.INSTANCE));
        widget.setAppearanceCharacteristics(fieldAppearance);

        widget.setPrinted(true);

        page.getAnnotations().add(widget);

        textField.setValue("Sample Field");

        pdDocument.save("d:/temp/sample_form.pdf");
        pdDocument.close();
    }
}
</code>
</pre>
