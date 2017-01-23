---
layout: home
title: Apache PDFBox Tutorial
comments: true
PAGE_IDENTIFIER: password_protection
---

<div class="demo-crumbs mdl-color-text--grey-500">
  Home &gt; Password Protection
</div>

### Password Protection

While PDF format makes it excellent choice to share documents and electronic forms
with users, sometimes there is need to protect PDF contents from strangers. There
are numerous situations including PDF containing confidential information like
Salary details, Insurance policy details or a confidential contract etc. To mitigate
such requirements, only the parties knowing a mutually trusted password should be
able to see the contents.

PDFBox provides APIs to set two different passwords,

1. **Owner Password**
  If owner password is entered, when prompted, user will be granted all the Permissions
  including extracting, printing contents etc.

2. **User Password**
  If user password is entered, when prompted, user will be granted only those Permissions
  which are exclusively granted.

Refer below code which configures Access permissions using password for both
*Owner* and *User*.

<pre>
<code class="java">
AccessPermission permission = new AccessPermission();
permission.setCanPrint(false);
permission.setCanExtractContent(false);

StandardProtectionPolicy policy = new StandardProtectionPolicy("ownerpdf", "userpdf", permission);
pdDoc.protect(policy);
</code>
</pre>

It is mandatory to create an instance of *AccessPermission* and pass it to the
*StandardProtectionPolicy* instance. For illustration purpose, above code snippet
sets Print and content extraction permissions to false for user other than owner himself.

While opening the PDF, a password prompt will appear. If **userpdf** is entered
as password, user won't be able to print the PDF document or extract the contents.
To gain access to print PDF, **ownerpdf** should be entered as password. Note that
either of the above passwords are optional.
