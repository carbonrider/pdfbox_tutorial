---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: merge_pdf
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Merging PDF
</div>

### Merging PDF
Merging PDFs with PDFBox is very simple. The readymade API *PDFMergerUtility*
provides convenient methods to specify files to be merged and a destination where
the merged PDF should be written.

Refer below code snippet, which merges two PDFs.

<pre>
<code class="java">
public class PDFMerge {
    public static void main(String[] args) throws Exception{
        PDFMergerUtility pdfUtility = new PDFMergerUtility();
        pdfUtility.addSource(new File("d:/temp/simple.pdf"));
        pdfUtility.addSource(new File("d:/temp/with_font_pdf.pdf"));
        pdfUtility.setDestinationFileName("d:/temp/merged.pdf");

        MemoryUsageSetting setting = MemoryUsageSetting.setupMainMemoryOnly();
        pdfUtility.mergeDocuments(setting);
    }
}
</code>
</pre>

Instantiate *PDFMergerUtility* and invoke *addSource* method to specify the files
to be merged. Specify the location of merged file, use *setDestinationFileName*.

Later, invoke *mergeDocuments* which requires memory settings to produce the merged
file.
