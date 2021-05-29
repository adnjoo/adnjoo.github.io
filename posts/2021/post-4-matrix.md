---
layout: post-layout.njk
title: matrix
date: 2021-05-28
tags: ['post']

---
<!-- Excerpt Start -->
<div id='hideme'>
fun little matrix thing
</div>
<!-- Excerpt End --> 

<body style="background-color:black; color: green; font-size: 40px">
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