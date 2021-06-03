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

using <a href='https://momentjs.com/'>moment.js</a>

What is time? It is a serpent which eats its tail [...]. - K. V.

<style>

    .face::after {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 12px;
      height: 12px;
      margin: -6px 0 0 -6px;
      background: black;
      border-radius: 6px;
      content: "";
      display: block;
    
    }

    #over {
        transform: translate(0,300px);
    }
    .circle {
        
        width: 180px;
        height: 180px;
        margin: 0 auto;
        border: 8px solid black;
        border-radius: 50%;
        transform:translate(0,-100px)
    }
    #second, #minute, #hour {
      transform-origin: 50% 100%;
      margin: -40% -1px 0 0;
      padding: 40% 1px 0;
      width: 0;
      height: 0;
      position: absolute;
      top: 50%;
      left: 50%;
      background: black;
      border-radius: 4px 0 0 4px;
    }
    #hour {
      margin: -4px 0 -4px -25%;
      padding: 4px 0 4px 25%;
      transform-origin: 100% 50%;
    }
    #minute {
      margin: -40% -3px 0;
      padding: 40% 3px 0;
    }
    #second {
      margin: -40% -1px 0 0;
      padding: 40% 1px 0;
    }
    footer {
      transform: translate(0,200px);
    }
    </style>
   

<body>
        <div id='over'>
            <div class="circle">
                <div class='face'>
                    <div id="hour" class="hour"></div>
                    <div id="minute" class="minute"></div>
                    <div id="second" class="second"></div>
                </div>
            </div>
        </div>
    <script>
        $(function() {
        function updateClock(){
            var now = moment(),
                second = now.seconds() * 6,
                minute = now.minutes() * 6 + second / 60,
                hour = ((now.hours() % 12) / 12) * 360 + 90 + minute / 12;
            $('#hour').css("transform", "rotate(" + hour + "deg)");
            $('#minute').css("transform", "rotate(" + minute + "deg)");
            $('#second').css("transform", "rotate(" + second + "deg)");
        }
        setInterval(updateClock, 100);
    });
    </script>
</body>