---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: page_size
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Page Size
</div>

### Page Size

In real world, documents created using PDF libraries may require an additional
feature of setting custom page size. Fortunately PDFBox comes with API to specify
page size as per standard units referred in day to day business. The page size
are A0, A1, ..., A6, LEGAL and LETTER.

<pre>
<code class="java">
public class PageSize {

  /**
   * Creates PDF with different page size.
   *
   * @param args
   * @throws Exception
   */
  public static void main(String[] args) throws Exception {
    PDDocument pdfDoc = new PDDocument();

    PDPage page = createPage(PDRectangle.A0);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A0");

    page = createPage(PDRectangle.A1);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A1");

    page = createPage(PDRectangle.A2);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A2");

    page = createPage(PDRectangle.A3);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A3");

    page = createPage(PDRectangle.A4);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A4");

    page = createPage(PDRectangle.A5);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A5");

    page = createPage(PDRectangle.A6);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "A6");

    page = createPage(PDRectangle.LEGAL);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "LEGAL");

    page = createPage(PDRectangle.LETTER);
    pdfDoc.addPage(page);
    writeTextToPage(pdfDoc, page, "LETTER");

    pdfDoc.save("d:/temp/page_size.pdf");
    pdfDoc.close();
  }

  /**
   * Creates new page with specified size.
   *
   * @param size Size for new page.
   * @return Returns page instance.
   */
  private static PDPage createPage(PDRectangle size) {
    return new PDPage(size);
  }

  /**
   * Writes given text to PDF page.
   *
   * @param pdfDoc An instance of PDF Document.
   * @param page   An instance of PDF Page.
   * @param text   Text to be written.
   */
  private static void writeTextToPage(PDDocument pdfDoc, PDPage page, String text) throws Exception {
    int textPosition = (int)(page.getBBox().getHeight() * (60f/100f));
    PDPageContentStream stream = new PDPageContentStream(pdfDoc, page);
    stream.beginText();
    stream.setFont(PDType1Font.HELVETICA, 12);
    stream.newLineAtOffset(10, textPosition);
    stream.showText(text);
    stream.endText();
    stream.close();
  }
}
</code>
</pre>

Have a look at the *createPage* method. It specifies the desired page size while
creating the *PDPage* instance. Also you will notice that *writeTextToPage* method
calculates offset for text (60% from bottom), based on the size of the page.
Since the page dimensions will differ for each page, the calculation is done
based on the height retrieved using *page.getBBox().getHeight()* API.
