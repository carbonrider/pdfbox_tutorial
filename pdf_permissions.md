---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: permissions
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Permissions
</div>


### Permissions

PDF document is in read only mode, if opened with Acrobat reader. If you wish to
edit the document, then special software is required to edit the contents.
Additionally, if you desire that your users should not be able to print the contents
nor should be able to extract the contents, you should enable permissions on the
document.

PDFBox provides convenient API to achieve above mentioned requirement - *AccessPermission*.

<pre>
<code class="java">
AccessPermission permission = new AccessPermission();
permission.setCanPrint(false);
permission.setCanExtractContent(false);

StandardProtectionPolicy policy = new StandardProtectionPolicy("", "", permission);
pdDoc.protect(policy);
</code>
</pre>

Above code doesn't grant Print or content extraction permissions to users. The permissions
are configured using *StandardProtectionPolicy*. Note that first two arguments are
passed with blank string argument. This indicates that PDF is not password protected
and anyone can view the contents but cannot print or extract it.
