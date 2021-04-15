---
layout: post-layout.njk
title: random quote
date: 2021-03-27
tags: ['post']

---
<!-- Excerpt Start -->
testing [quotable.io](https://quotable.io) api
<!-- Excerpt End --> 

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
function get_quote() {
    $.get("https://api.quotable.io/random", function(data){
      document.getElementById('para').innerHTML = data.content;
      document.getElementById('author').innerHTML = data.author;
    });
}

$(document).ready(function(){
  get_quote();
  $("button").click(function(){
    get_quote();
  });
});

</script>
</head>
<body>

<div id="para">
</div>

<div id="author">
</div>

<button>Random quote</button>
