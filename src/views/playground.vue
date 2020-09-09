<template>
  <div class="playground" ref="test">
    <canvas id="canvas" width="500" height="800" />
  </div>
</template>

<script>
/* eslint-disable */
class Text {
  constructor (x, y, speed, content) {
    // TODO: 50
    this.x = x + (50 * Math.random())
    this.y = y
    this.speed = speed * (Math.random() + 0.5)
    this.content = content
    this.direction = 1
  }
}

export default {
  data() {
    return {
      /** @type {HTMLCanvasElement} **/
      canvas: null,
      /** @type {CanvasRenderingContext2D} **/
      ctx: null,
      text: "09103921312312312312312312312312",
      textArray: []
    };
  },
  mounted() {
    this.canvas = document.getElementById("canvas");
    this.ctx = this.canvas.getContext("2d");
    // this.ctx.translate(0, this.canvas.height)
    // this.ctx.scale(1, -1)
    const canvasWidth = this.canvas.width;
    const canvasHeight = this.canvas.height;
    const textCount = 5
    for (let i = 0; i < textCount; i++) {
      this.textArray.push(new Text(canvasWidth / textCount * i, canvasHeight, 1.5, '123123123'));
    }
    this.render(this.ctx)
    setInterval(() => {
      this.render(this.ctx)
    }, 16)
  },

  methods: {
    render (ctx) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      this.textArray.map(textInstance => {
        this.drawText(ctx, textInstance.x, textInstance.y);
        textInstance.y -= textInstance.speed * textInstance.direction
        if (textInstance.y < -50 || textInstance.y > this.canvas.height) {
          textInstance.direction *= -1
        }
      })
    },
    /**
     * @param {CanvasRenderingContext2D} ctx
     */
    drawText(ctx, x, y) {
      ctx.save();
      ctx.translate(x, y);
      ctx.rotate((90 * Math.PI) / 180);
      ctx.font = "24px sans-serif";
      ctx.fillText(this.text, 0, 0);
      ctx.restore();
    }
  }
};
</script>

<style scoped>
.playground {
  background-color: white;
  height: 100vh;
  width: 100vw;
}
#canvas {
  background-color: transparent;
}
</style>
