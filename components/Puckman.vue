<template>
  <div>
    <button class="puckman-start" @click="insertCoin" v-if="!gameOn">Start Puckman</button>
    <div 
      class="puckman"
      v-if="gameOn"
      ref="puckman"
      :style="{
        left: puckman.x + 'px',
        top: puckman.y + 'px',
        width: puckman.size + 'px',
        height: puckman.size + 'px' }" 
      />
  </div>
</template>

<script>
export default {
  data() {
    return {
      puckman: {
        x: 0,
        y: 0,
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


          // console.log(puckman.getBoundingClientRect());
          this.checkForElementToDestroy(newX, newY);

          this.puckman.x = newX;
          this.puckman.y = newY;
        }

      });
    },

    checkForElementToDestroy: function(x, y) {
      // const { x, y } = this.puckman;
      console.log(x, y);
      const { size } = this.puckman;
      const overlappingElements = [
        document.elementFromPoint(x, y),
        document.elementFromPoint(x + size, y),
        document.elementFromPoint(x + size, y + size),
        document.elementFromPoint(x, y + size),
        document.elementFromPoint(x + size / 2, y + size / 2)
      ];

      const uniqueOverlappingElements = overlappingElements.filter(function(item, i, ar) {
        return ar.indexOf(item) === i && item.children.length === 0 && item.className !== 'puckman';
      });

      console.log('uniqueOverlappingElements', uniqueOverlappingElements);
      uniqueOverlappingElements.forEach(element => {
        element.parentNode.removeChild(element);
      })
      
    }
  }
}
</script>

<style>
.puckman {
  display: block;
  border-radius: 50%;
  background: yellow;
  border: 1px solid #444;
  position: absolute;
  transition: .1s all;
}
</style>
