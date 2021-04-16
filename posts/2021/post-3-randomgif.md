---
layout: post-layout.njk
title: random gif
date: 2021-04-15
tags: ['post']

---
<!-- Excerpt Start -->
random gif :: testing [giphy](https://giphy.com) api
<!-- Excerpt End --> 



random gif
<img id='img' src=''>



<script>
var x='https://media2.giphy.com/media/'
var y
var z
fetch('https://api.giphy.com/v1/gifs/trending?api_key=UJHVXZkSLWFZeooBpe9DpTvP0Aft7czt')
.then(response => response.json())
  .then(data => {
    y = data
    z = Math.floor(Math.random() * 50);
    x += y.data[z].id+'/giphy.gif';
    console.log(data)
    document.getElementById("img").src = x
  });
</script>
