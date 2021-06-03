---
layout: post-layout.njk
title: matrix
date: 2021-05-28
tags: ['post']

---
<!-- Excerpt Start -->
<p id='hideme'>
fun little matrix thing
</p>
<!-- Excerpt End -->

<style>
/* div, article, main, p, footer, body */
span{
    border: 1px solid transparent;
}
p {
    font-size: 30px
}
</style>
<body style="background-color:black; color: green">
<div style="transform: translate(50px,0px)">
<div id="typed-strings">
    <p>Wake up, Neo...</p>
    <p>The Matrix has you...</p>
    <p>Follow the white rabbit.</p>
    <p>Knock, knock.</p>
    <p></p>
</div>

<span id="typed"></span>

</div>

</body>
</script>
<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>
<script>
    var x = document.getElementById("hideme");
    x.style.display = "none";
    var typed = new Typed('#typed', {
    stringsElement: '#typed-strings',
    typeSpeed: 70,
    backSpeed: 30,
    showCursor: false,
    loop:true
    });
</script>
