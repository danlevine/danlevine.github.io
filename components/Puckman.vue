<template>
  <div>
    <button
      class="puckman-start-btn"
      @click="insertCoin"
    />
    <div
      class="puckman"
      v-if="gameOn"
      ref="puckman"
      :style="{
        left: puckman.x + 'px',
        top: puckman.y + 'px',
        width: puckman.size + 'px',
        height: puckman.size + 'px' }" 
      >
        <div class="puckman__top" />
        <div class="puckman__bottom" />
        <div class="puckman__cover" />
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      puckman: {
        x: 15,
        y: 15,
        size: 20
      },
      gameOn: false
    }
  },
  methods: {
    insertCoin: function() {
      if (this.gameOn) return; // return if game already started

      console.log('game on!');
      this.gameOn = true;
      document.addEventListener('keydown', e => {
        const keyCode = e.keyCode;
        const { puckman } = this.$refs;

        const keyMap = {
          left: 37,
          up: 38,
          right: 39,
          down: 40
        };

        if ([37, 38, 39, 40].indexOf(keyCode) !== -1) {
          const oldX = this.puckman.x;
          const oldY = this.puckman.y;
          let newX = oldX;
          let newY = oldY;

          const increment = 15;
          if (keyCode === keyMap["left"]) newX = oldX - increment;
          else if (keyCode === keyMap["up"]) newY = oldY - increment;
          else if (keyCode === keyMap["right"]) newX = oldX + increment;
          else if (keyCode === keyMap["down"]) newY = oldY + increment;

          this.checkForElementToDestroy(newX, newY);

          this.puckman.x = newX;
          this.puckman.y = newY;
        }

      });
    },

    checkForElementToDestroy: function(x, y) {
      const { size } = this.puckman;
      const overlappingElements = [
        document.elementFromPoint(x, y),
        document.elementFromPoint(x + size, y),
        document.elementFromPoint(x + size, y + size),
        document.elementFromPoint(x, y + size),
        document.elementFromPoint(x + size / 2, y + size / 2)
      ];

      const uniqueOverlappingElements = overlappingElements.filter(function(item, i, ar) {
        return ar.indexOf(item) === i && item.children.length === 0 && !item.className.includes('puckman');
      });

      console.log('uniqueOverlappingElements', uniqueOverlappingElements);
      uniqueOverlappingElements.forEach(element => {
        element.parentNode.removeChild(element);
      })
      
    }
  }
}
</script>

<style lang="scss">
$btn-color: hsla(10, 90%, 40%, 1);
$btn-size: 25px;

.puckman {
  display: block;
  position: absolute;
  transition: .1s all;
  animation: slide-in-left 1s ease-out;
}

.puckman-start-btn {
  position: absolute;
  bottom: 20px;
  right: 20px;
  width: $btn-size;
  height: $btn-size;
  border: 0;
  margin: 1em;
  outline: none;
  background-color: $btn-color;
  border-radius: 50%;
  cursor: pointer;
  transition: box-shadow 200ms;

  box-shadow: 
    inset 0 $btn-size/32 0 lighten($btn-color, 5%),
    inset 0 (-$btn-size/32) 0 darken($btn-color, 5%),
    inset 0 0 0 $btn-size/32 darken($btn-color, 3%),
    inset 0 0 0 $btn-size/12 $btn-color,
    inset 0 0 0 $btn-size/10 darken($btn-color, 20%),
    inset 0 0 0 $btn-size/9.2 darken($btn-color, 50%),
    inset 0 0 0 $btn-size/7.5 transparentize(lighten($btn-color, 30%), .3),
    inset 0 0 0 $btn-size/5.5 $btn-color,
    inset 0 $btn-size/2.5 $btn-size/7.5 darken($btn-color, 5%),
    inset 0 0 $btn-size/10 $btn-size/6 darken($btn-color, 10%),
    0 $btn-size/20 0 rgba(0, 0, 0, .3);

  &:after {
    content: '';
    position: absolute;
    bottom: $btn-size/20;
    left: $btn-size/10;
    display: block;
    width: $btn-size/1.25;
    height: $btn-size/1.25;
    border: $btn-size/15 solid rgba(0, 0, 0, .3);
    border-width: 0 0 $btn-size/15;
    border-radius: 50%;
    transition-duration: 200ms;
  }

  &:active,
  &.is-pushed {
    box-shadow: 
      inset 0 $btn-size/32 0 lighten($btn-color, 5%),
      inset 0 (-$btn-size/32) 0 darken($btn-color, 5%),
      inset 0 0 0 $btn-size/32 darken($btn-color, 3%),
      inset 0 0 0 $btn-size/12 $btn-color,
      inset 0 0 0 $btn-size/10 darken($btn-color, 20%),
      inset 0 0 0 $btn-size/8.5 darken($btn-color, 40%),
      inset 0 0 0 $btn-size/7.5 transparentize(lighten($btn-color, 30%), .8),
      inset 0 0 0 $btn-size/5.5 darken($btn-color, 3%),
      inset 0 $btn-size/2.5 $btn-size/7.5 darken($btn-color, 8%),
      inset 0 0 $btn-size/10 $btn-size/6 darken($btn-color, 15%),
      0 $btn-size/20 0 rgba(0, 0, 0, .3);
    background-color: darken($btn-color, 2%);
        
    &:after {
      bottom: $btn-size/20 + $btn-size/15;
      border-width: 0;
    }
  }
}

.puckman div {
  position: absolute;
  width: 20px;
  height: 10px;
  border-radius: 120px 120px 0 0;
  background: #ffff00;
}

.puckman__top,
.puckman__bottom {
  animation: puckman-top .8s linear infinite;
  transform-origin: 10px 10px;
  border: 1px solid hsl(60, 100%, 35%);
}

.puckman__bottom {
  animation: puckman-bottom .8s linear infinite;
}

.puckman__cover {
  transform: rotate(270deg) translateX(-13.5px) translateY(5px) scale(0.85);
  transform-origin: 0;
}

@keyframes puckman-top {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(-45deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
@keyframes puckman-bottom {
  0% {
    transform: rotate(180deg);
  }
  50% {
    transform: rotate(225deg);
  }
  100% {
    transform: rotate(180deg);
  }
}

@keyframes slide-in-left {
  0% {
    left: -40px;
  }
  100% { 
    left: 15px;
   }
}

</style>
