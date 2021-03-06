---
layout: post-layout.njk
idx: 10
title: endless runner
date: 2019-11-14
tags: ['post']
---
<!-- Excerpt Start -->
endless runner game using phaser.js
<!-- Excerpt End -->

<style type = "text/css">

@media only screen and (max-width: 600px) {
body {
width:90%
}
}
</style>

<script src = "https://cdnjs.cloudflare.com/ajax/libs/phaser/3.24.1/phaser.min.js"></script>
<script>
let game;

var score = 0;
var scoreText;


// global game options
let gameOptions = {
    platformStartSpeed: 350,
    spawnRange: [150, 300],
    platformSizeRange: [70, 250],
    playerGravity: 900,
    jumpForce: 400,
    playerStartPosition: 200,
    jumps: 2
}

window.onload = function() {

    // object containing configuration options
    let gameConfig = {
        type: Phaser.AUTO,
        width: 1334,
        height: 750,
        scene: playGame,
        backgroundColor: 0xfffbf8,

        // physics settings
        physics: {
            default: "arcade"
        }
    }
    game = new Phaser.Game(gameConfig);
    window.focus();
    resize();
    window.addEventListener("resize", resize, false);
}

// playGame scene
class playGame extends Phaser.Scene{
    constructor(){
        super("PlayGame");
    }
    preload(){
        this.load.image("platform", "https://i.postimg.cc/mDw64Jdm/platform.png");
        this.load.image("player", "https://i.postimg.cc/9FzN3xyB/Untitled.jpg");
    }
    create(){

      scoreText = this.add.text(16, 16, 'score: 0', { fontSize: '32px', fill: '#000' });

        // group with all active platforms.
        this.platformGroup = this.add.group({

            // once a platform is removed, it's added to the pool
            removeCallback: function(platform){
                platform.scene.platformPool.add(platform)
            }
        });

        // pool
        this.platformPool = this.add.group({

            // once a platform is removed from the pool, it's added to the active platforms group
            removeCallback: function(platform){
                platform.scene.platformGroup.add(platform)
            }
        });

        // number of consecutive jumps made by the player
        this.playerJumps = 0;

        // adding a platform to the game, the arguments are platform width and x position
        this.addPlatform(game.config.width, game.config.width / 2);

        // adding the player;
        this.player = this.physics.add.sprite(gameOptions.playerStartPosition, game.config.height / 2, "player");
        this.player.setGravityY(gameOptions.playerGravity);

        // setting collisions between the player and the platform group
        this.physics.add.collider(this.player, this.platformGroup);

        // checking for input
        this.input.on("pointerdown", this.jump, this);
        this.input.keyboard.on('keydown', this.jump, this);

    }

    // the core of the script: platform are added from the pool or created on the fly
    addPlatform(platformWidth, posX){
        let platform;
        if(this.platformPool.getLength()){
            platform = this.platformPool.getFirst();
            platform.x = posX;
            platform.active = true;
            platform.visible = true;
            this.platformPool.remove(platform);
        }
        else{
            platform = this.physics.add.sprite(posX, game.config.height * 0.8, "platform");
            platform.setImmovable(true);
            platform.setVelocityX(gameOptions.platformStartSpeed * -1);
            this.platformGroup.add(platform);
        }
        platform.displayWidth = platformWidth;
        this.nextPlatformDistance = Phaser.Math.Between(gameOptions.spawnRange[0], gameOptions.spawnRange[1]);
    }

    // the player jumps when on the ground, or once in the air as long as there are jumps left and the first jump was on the ground
    jump(){
        if(this.player.body.touching.down || (this.playerJumps > 0 && this.playerJumps < gameOptions.jumps)){
            if(this.player.body.touching.down){
                this.playerJumps = 0;
            }
            this.player.setVelocityY(gameOptions.jumpForce * -1);
            this.playerJumps ++;
            score += 10;
            scoreText.setText('Score: ' + score);

        }
    }
    update(){

        // game over
        if(this.player.y > game.config.height){
            this.scene.start("PlayGame");
            score =0;
        }
        this.player.x = gameOptions.playerStartPosition;

        // recycling platforms
        let minDistance = game.config.width;
        this.platformGroup.getChildren().forEach(function(platform){
            let platformDistance = game.config.width - platform.x - platform.displayWidth / 2;
            minDistance = Math.min(minDistance, platformDistance);
            if(platform.x < - platform.displayWidth / 2){
                this.platformGroup.killAndHide(platform);
                this.platformGroup.remove(platform);
            }
        }, this);

        // adding new platforms
        if(minDistance > this.nextPlatformDistance){
            var nextPlatformWidth = Phaser.Math.Between(gameOptions.platformSizeRange[0], gameOptions.platformSizeRange[1]);
            this.addPlatform(nextPlatformWidth, game.config.width + nextPlatformWidth / 2);
        }
    }
};
function resize(){
      let canvas = document.querySelector("canvas");
  if( /Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent) ) {
  console.log('running on phone');console.log('phone width')
  let windowWidth = 350;
  console.log(windowWidth);
  let windowHeight = 650;
  console.log(windowHeight);
  let windowRatio = windowWidth / windowHeight;
  let gameRatio = game.config.width / game.config.height;
  if(windowRatio < gameRatio){
      canvas.style.width = windowWidth + "px";
      canvas.style.height = (windowWidth / gameRatio) + "px";
  }
  else{
      canvas.style.width = (windowHeight * gameRatio) + "px";
      canvas.style.height = windowHeight + "px";
  }
  return;
}
console.log('im still running')
    let windowWidth = window.innerWidth;
    console.log('browser width'+windowWidth);
    let windowHeight = window.innerHeight;
    console.log(windowHeight);
    let windowRatio = windowWidth / windowHeight;
    let gameRatio = game.config.width / game.config.height;
    if(windowRatio < gameRatio){
        canvas.style.width = windowWidth + "px";
        canvas.style.height = (windowWidth / gameRatio) + "px";
    }
    else{
        canvas.style.width = (windowHeight * gameRatio) + "px";
        canvas.style.height = windowHeight + "px";
    }


}

</script>
