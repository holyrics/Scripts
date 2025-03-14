# Styled Text
To display text with advanced formatting, start the text with **&lt;styled&gt;**

HTML tags available

```html
<styled>
<b>bold</b>
<i>italic</i>
<u>underlined</u>
<color:0000FF>Font color</color>
<font:Arial>Font name</font>
<size:70>Relative font size 70%</size>

From v2.23.0
<line-height:100>Line height</line-height>
<valign:0>Vertical alignment  -200 ~ 200  </valign>
<bgcolor:000000>Background color</bgcolor>
<brightness-color:000000>Glow color</brightness-color>
<brightness-weight:50>  0 ~ 100  </brightness-weight>
<outline-color:000000>Outline color</outline-color>
<outline-weight:50>  0 ~ 100  </outline-weight>
<shadow-color:000000>Shadow color</shadow-color>
<shadow-x-weight:50>  -100 ~ 100  </shadow-x-weight>
<shadow-y-weight:-50>  -100 ~ 100  </shadow-y-weight>
<blur>Apply blur effect</blur>
```

---

## v2.25.0+

It is possible to create formatting models (similar to how CSS works) to reuse the respective formatting in texts displayed in different locations of the program compatible with the &lt;styled&gt; syntax

**Example:**
```
title {
  b;
  size: 120;
}

footer {
  i;
  size: 80;
}
```

**Text:**
```
<#:title>Example</#>
 
Example Example Example Example
```

The text inside the tag `<#:title>...</#>` will be displayed in bold formatting and a relative font size of 120%.
