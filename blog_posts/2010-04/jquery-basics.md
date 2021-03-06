Id: 108001
Title: jQuery basics
Tags: javascript,jquery,note
Date: 2010-04-29T12:51:42-07:00
Format: Markdown
--------------
Running initialization code:\
<code>\
\$(document).ready(function(){\
 // your init code here\
});\
</code>

Selecting elements

<code>\
var els = \$(“\#myid”); // all elements having id “myid”\
var els = \$(“[txt]”); // elements with attribute txt\
</code>

Modifying content

<code>\
els.addClass(“hide”);\
els.removeClass(“hide”);\
els.hasClass(“hide”); // true if at least one element has this class\
var attr = el.attr(“myattr”); // value of attribute “myattr”\
el.attr(“myattr”, “attrval”); // set value of attribute “myattr” to
“attrval”\
var txt = els.text();\
els.text(“new text”);\
els.replaceWith(“txt”); // replace element with “txt”\
</code>

Enable/disable element

<code>\
\$(“\#id”).attr(“disabled”,“disabled”);\
\$(“\#id”).removeAttr(“disabled”);\
</code>

Misc

<code>\
\$(“\#id”).focus() - to focus on a given element e.g. text input
element\
</code>

Handling radio buttons

<code>\
\$(“\#id”).attr(“checked”, “checked”); // select a radio button\
</code>

Handling checkboxes

<code>\
\$(“\#id”).is(“:checked”) - returns true if a checkbox button is
checked\
</code>
