# testerrss
<!DOCTYPE html>

<html>

     <meta name="HandheldFriendly" content="true" />

<meta name="viewport"

          content="width=device-width,

                 height=device-height, user-scalable=no" />

    

 

<div class='stage-home'>

  <br>

  <br>

  <h1 class='blue'>Two cube</h1>

  <h1 class='red'>Confusion</h1>

  <div class='logo'></div>

</div>

<div class='stage-play'>

  <h1 class='points'>0</h1>

  <div class='mask'></div>

  <div class='btn left'></div>

  <div class='btn right'></div>

</div>

<div class='stage-gameover'>

  <br>

  <br>

  <h1 class='blue'>Your Score:</h1>

  <h1 class='red points'></h1>

  <div class='logo'></div>

</div>

<head>

<title>Cubes confusionss</title>

</head>

<body>




</body>


<style>

@import url(http://fonts.googleapis.com/css?family=Open+Sans);

* {

  margin: 0;

  padding: 0;

  border: 0;

  outline: 0;

  box-sizing: border-box;

}


html, body {

  height: 100%;

}


body {

  background-color: #2c3e50;

  font-family: 'Open Sans', snas-serif;

  font-size: 1em;

  color: #fff;

}


.red {

  color: #BDBDBD;

}


.blue {

  color: #3498db;

}


[class*='stage-'] {

  width: 300px;

  height: 500px;

  border: 0px solid #34495e;

  position: absolute;

  top: 0;

  left: 0;

  right: 0;

  bottom: 0;

  margin: auto;

  display: none;

  text-align: center;

  border-radius: 5px;

  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.15);

  overflow: hidden;

}

[class*='stage-'] .logo {

  width: 150px;

  height: 150px;

  border-top: 10px solid #3498db;

  border-right: 10px solid #3498db;

  border-left: 10px solid #BDBDBD;

  border-bottom: 10px solid #BDBDBD;

  border-radius: 10%;

  transform: rotate(-45deg);

  margin: 50px auto;

  cursor: pointer;

  position: relative;

  transition: all .3s ease;

}

[class*='stage-'] .logo:before {

  content: "";

  position: absolute;

  border-left: 50px solid #fff;

  border-top: 25px solid transparent;

  border-bottom: 25px solid transparent;

  transform: rotate(45deg);

  top: 50%;

  left: 50%;

  margin-left: -20px;

  margin-top: -20px;

}

[class*='stage-'] .logo:hover {

  transform: scale(1.1) rotate(-45deg);

}

[class*='stage-'].stage-home {

  display: block;

}

[class*='stage-'].stage-play .mask {

  position: absolute;

  z-index: 1;

  width: 100%;

  height: 20%;

  background-color: #2c3e50;

  bottom: 0;

  left: 0;

}

[class*='stage-'].stage-play .btn {

  width: 60px;

  height: 60px;

  background-color: #2c3e50;

  border-radius: 20%;

  position: absolute;

  z-index: 2;

  bottom: 8.5%;

  border-top: 5px solid #3498db;

  border-right: 5px solid #BDBDBD;

  border-left: 5px solid #BDBDBD;

  border-bottom: 5px solid #3498db;

  transform: rotate(-1deg);

  cursor: pointer;

  transition: all .3s ease;

}

[class*='stage-'].stage-play .btn.red {

  transform: rotate(90deg);

}

[class*='stage-'].stage-play .btn.left {

  left: 52px;

}

[class*='stage-'].stage-play .btn.right {

  right: 52px;

}

[class*='stage-'].stage-play .dots {

  position: absolute;

  width: 150px;

  height: 20px;

  top: -20px;

  left: 0;

  right: 0;

  margin: 0 auto;

  z-index: 0;

}

[class*='stage-'].stage-play .dots .dot {

  position: absolute;

  width: 20px;

  height: 20px;

  border-radius: 20%;

}

[class*='stage-'].stage-play .dots .dot:first-of-type {

  left: 0;

}

[class*='stage-'].stage-play .dots .dot:last-of-type {

  right: 0;

}

[class*='stage-'].stage-play .dots .dot.red {

  background-color: #BDBDBD;

}

[class*='stage-'].stage-play .dots .dot.blue {

  background-color: #3498db;

}


</style>





<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"> </script>


<script>  (function() {

  var game;


  $(document).ready(function() {

    return game.init();

  });


  game = {

    points: 0,

    left: "blue",

    right: "blue",

    speed: 4000,

    game_interval: "",

    init: function() {

      return this.bind_events();

    },

    bind_events: function() {

      $(document).on("click", ".logo", function(e) {

        e.preventDefault();

        game.switch_stage("play");

        return game.start();

      });

      return $(document).on("click", ".btn", function(e) {

        e.preventDefault();

        return $(this).toggleClass("red");

      });

    },

    switch_stage: function(stage) {

      if (stage === "gameover") {

        $(".dots").remove();

        clearInterval(this.game_interval);

      }

      $("[class*='stage-']").hide();

      return $(".stage-" + stage).show();

    },

    start: function() {

      this.points = 0;

      this.left = "blue";

      this.right = "blue";

      $(".points").html("0");

      $(".btn").removeClass("red");

      return this.game_interval = setInterval(function() {

        return game.generate_dots();

      }, 1500);

    },

    generate_dots: function() {

      var colors, dot1, dot2, dots;

      dots = $("<div class='dots'></div>");

      colors = ["red", "blue"];

      dot1 = $("<div class='dot " + colors[Math.floor(Math.random() * colors.length)] + "'></div>");

      dot2 = $("<div class='dot " + colors[Math.floor(Math.random() * colors.length)] + "'></div>");

      dots.append(dot1);

      dots.append(dot2);

      $(".stage-play").append(dots);

      return dots.animate({

        top: "80%"

      }, this.speed, "linear", function() {

        

        if ($(".btn.left").hasClass("red")) {

          if ($(".dot:first-of-type", this).hasClass("blue")) {

            game.switch_stage("gameover");

          }

        }

        

        if ($(".btn.right").hasClass("red")) {

          if ($(".dot:last-of-type", this).hasClass("blue")) {

            game.switch_stage("gameover");

          }

        } 

           if ($(".btn.left").hasClass("red")) {

          if ($(".dot:first-of-type", this).hasClass("red")) {

             game.add_points();

          }

        } 

        

        if ($(".btn.right").hasClass("red")) {

          if ($(".dot:last-of-type", this).hasClass("red")) {

             game.add_points();

          }

        } 

          

        return $(this).remove();

      });

    },

    add_points: function() {

      this.points += 1;

      return $(".points").html(this.points);

    }

  };


}).call(this); </script>

</html>
