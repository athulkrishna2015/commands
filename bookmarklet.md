# How can we copy text from Wikipedia without the citation parts “[1]”, “[2]”, “[3]”


Create a new browser bookmark and copy the javascript code below into it - when you want to copy some text from wikipedia, just click it beforehand and it'll remove all instances of [n] to meet your requirement in the question.

`javascript:function a (){document.body.innerHTML=document.body.innerHTML.replace(/<sup\b[^>]*>(.*?)<\/sup>/gi, "" );return;}; a();`

Behind the scenes, it's just doing a regular expression search and replace of all <sup>...</sup> HTML tags on the page.

I've just tried this in IE7 and it works fine, so hopefully should be ok in other browsers too.

I'll credit this SO thread with pointing me in the right direction - I knew a bookmarklet was the way to go, but had never written one before.
