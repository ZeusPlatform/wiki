## figure
[figure](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure)
使用参考掘金文章
https://juejin.im/post/5cc5ad456fb9a032233532df

```html
<!-- Just an image -->
<figure>
  <img
  src="https://developer.mozilla.org/static/img/favicon144.png"
  alt="The beautiful MDN logo.">
</figure>

<!-- Image with a caption -->
<figure>
  <img
  src="https://developer.mozilla.org/static/img/favicon144.png"
  alt="The beautiful MDN logo.">
  <figcaption>MDN Logo</figcaption>
</figure>
<!-- code snippet -->
<figure>
  <figcaption>Get browser details using <code>navigator</code>.</figcaption>
  <pre>
function NavigatorExample() {
  var txt;
  txt = "Browser CodeName: " + navigator.appCodeName + "; ";
  txt+= "Browser Name: " + navigator.appName + "; ";
  txt+= "Browser Version: " + navigator.appVersion  + "; ";
  txt+= "Cookies Enabled: " + navigator.cookieEnabled  + "; ";
  txt+= "Platform: " + navigator.platform  + "; ";
  txt+= "User-agent header: " + navigator.userAgent  + "; ";
  console.log("NavigatorExample", txt);
}
  </pre>
</figure>
<!-- quotation -->
<figure>
  <figcaption><cite>Edsger Dijkstra:</cite></figcaption>
  <blockquote>If debugging is the process of removing software bugs,
  then programming must be the process of putting them in.</blockquote>
</figure>

<!-- poems-->
<figure>
  <p style="white-space:pre">
Bid me discourse, I will enchant thine ear,
  Or like a fairy trip upon the green,
Or, like a nymph, with long dishevell'd hair,
  Dance on the sands, and yet no footing seen:
Love is a spirit all compact of fire,
  Not gross to sink, but light, and will aspire.</p>
  <figcaption><cite>Venus and Adonis</cite>,
    by William Shakespeare</figcaption>
</figure>
```