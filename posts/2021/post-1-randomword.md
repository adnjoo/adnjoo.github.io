---
layout: post-layout.njk
title: random word
date: 2021-03-23
tags: ['post']

---
<!-- Excerpt Start -->
testing [wordnik](https://www.wordnik.com/) api
<!-- Excerpt End -->


<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
let data2 = 'a'
function get_word() {
      $.get("https://api.wordnik.com/v4/words.json/randomWords?hasDictionaryDef=true&minCorpusCount=0&minLength=5&maxLength=15&limit=1&api_key=a2a73e7b926c924fad7001ca3111acd55af2ffabf50eb4ae5", function(data){
        data2 = data[0].word;
        document.getElementById('para').innerHTML = data2;

        setTimeout(function(){
          $.get("https://api.wordnik.com/v4/word.json/"+data2+"/definitions?limit=200&includeRelated=false&useCanonical=false&includeTags=false&api_key=a2a73e7b926c924fad7001ca3111acd55af2ffabf50eb4ae5", function(data3){
            data4 = data3.map(x=>x.text).join(' ')
            document.getElementById('definition').innerHTML = data4;
          });
        }, 2000);
      });
}

$(document).ready(function(){
  get_word();
  $("button").click(function(){
    get_word()
  });
});
</script>
</head>
<body>

<div id="para">
</div>

<div id="definition">
</div>

<button>Random word</button>
