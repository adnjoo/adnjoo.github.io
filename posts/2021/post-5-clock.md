---
layout: post-layout.njk
title: clock
date: 2021-06-02
tags: ['post']

---
<!-- Excerpt Start -->

<p id="clock">loading ...</p>
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>

<script>
console.log(moment().format('MMMM Do YYYY, h:mm:ss a'))

function update() {
  $('#clock').html(moment().format('MMMM Do YYYY, h:mm:ss a'));
}

setInterval(update, 500);

</script>


<!-- Excerpt End -->

using moment.js

What is time? It is a serpent which eats its tail [...]. - K. V.