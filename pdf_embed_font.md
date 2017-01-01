---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: embed_font
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Embedding Fonts
</div>

### Embedding Fonts

There might be a need to add text with different font family and size. PDFBox supports
few fonts out of box and also has provision to load custom fonts. As of now, PDFBox
supports following fonts

- Courier
- Helvetica
- Times new roman

Font can be configured for text using *setFont* API available on Content Stream.

<pre>
<code class="java">
PDPageContentStream contentStream = new PDPageContentStream(pdDoc, pdPage);
...
contentStream.setFont(PDType1Font.HELVETICA, 12);
...
</code>
</pre>

Above example uses built-in font for displaying text. In case, if you want to render
text using custom font, refer below example.

<pre>
<code class="java">
public class EmbedFont {
    public static void main(String[] args) throws Exception{
        PDDocument pdDoc = new PDDocument();
        PDPage pdPage = new PDPage(PDRectangle.A4);
        addText(pdPage, pdDoc);
        pdDoc.addPage(pdPage);
        pdDoc.save("d:/temp/with_font_pdf.pdf");
        pdDoc.close();
    }

    private static void addText(PDPage pdPage, PDDocument pdDoc) throws IOException {
        PDPageContentStream contentStream = new PDPageContentStream(pdDoc, pdPage);
        contentStream.beginText();
        contentStream.newLineAtOffset(10, 500);
        contentStream.setFont(getFont(pdDoc),12);
        contentStream.showText("Hello World!!!");
        contentStream.endText();
        contentStream.close();
    }

    private static PDType0Font getFont(PDDocument pdDocument) throws IOException {
        PDType0Font font = PDType0Font.load(pdDocument, new File("d:/temp/Roboto-Light.ttf"));
        return font;
    }
}
</code>
</pre>

Font is loaded from a file using *PDType0Font* API.
