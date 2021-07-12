---
layout: post-layout.njk
title: random quote
date: 2021-03-27
tags: ["post"]
---

<!-- Excerpt Start -->

testing [quotes.rest](https://quotes.rest/) api

<!-- Excerpt End -->

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
function get_quote(url) {
    $.get(url, (data)=>{
      // console.log(data)
      document.getElementById('para').innerHTML = data.contents.quotes[0].quote;
      document.getElementById('author').innerHTML = data.contents.quotes[0].author;
    });
}

$(document).ready(()=>{
  get_quote("https://quotes.rest/qod?language=en");
});

</script>
</head>
<body>
<br>
Quote of the day
<div id="para">
</div>
<br>

<div id="author">
</div>
