<template>
    <div class="my-canvas">
        <canvas
            ref="canvas"
            class="canvas"
            :width="width"
            :height="height"
        ></canvas>
        <div class="canvas-img">
            <slot />
        </div>
    </div>
</template>

<script>
export default {
    name: "canvas-nyc",
    props: {
        width: {
            type: Number,
            default: 1820,
        },
        height: {
            type: Number,
            default: 260,
        },
        opt: {
            type: Object,
            default: () => ({}),
        },
    },
    created() {
        this.calcArc = {
            tr: this.calcArcTRLB,
            tl: this.calcArcTLBR,
            lb: this.calcArcTRLB,
            lt: this.calcArcLTBR,
            br: this.calcArcLTBR,
            bl: this.calcArcBLRT,
            rb: this.calcArcTLBR,
            rt: this.calcArcBLRT,
        };
        this.fillALL = {
            tl: this.drawFillTL,
            tr: this.drawFillTR,
            rb: this.drawFillRB,
            rt: this.drawFillRT,
            br: this.drawFillBR,
            bl: this.drawFillBL,
            lb: this.drawFillLB,
            lt: this.drawFillLT,
        };
    },
    methods: {
        //tr、lb 计算从上到右、从左到下的弧度
        calcArcTRLB(x, y, r) {
            return { x, y, x1: x + r, y1: y + r, r };
        },
        //tl、rb 计算从上到左、从右到下的弧度
        calcArcTLBR(x, y, r) {
            return { x, y, x1: x - r, y1: y + r, r };
        },
        //lt、br 计算从左到上、从下到右的弧度
        calcArcLTBR(x, y, r) {
            return { x, y, x1: x + r, y1: y - r, r };
        },
        //bl、rt 计算从下到左、从右到上的弧度
        calcArcBLRT(x, y, r) {
            return { x, y, x1: x - r, y1: y - r, r };
        },
        //画上右
        drawFillTR(rect, w, color) {
            const { x, y, r } = this.fillR(rect, w);
            const x1 = x - r;
            const y1 = y - r;
            this.drawFill(x, y1, x1, y1, r, color);
        },
        //画右下
        drawFillRB(rect, w, color) {
            const { x, y, r } = this.fillB(rect, w);
            const x1 = x + r;
            const y1 = y - r;
            this.drawFill(x1, y, x1, y1, r, color);
        },
        //画下左
        drawFillBL(rect, w, color) {
            const { x, y, r } = this.fillL(rect, w);
            const x1 = x + r;
            const y1 = y + r;
            this.drawFill(x, y1, x1, y1, r, color);
        },
        //画左上
        drawFillLT(rect, w, color) {
            const { x, y, r } = this.fillT(rect, w);
            const x1 = x - r;
            const y1 = y + r;
            this.drawFill(x1, y, x1, y1, r, color);
        },

        //画上左
        drawFillTL(rect, w, color) {
            const { x, y, r } = this.fillL(rect, w);
            const x1 = x + r;
            const y1 = y - r;
            this.drawFill(x, y1, x1, y1, r, color);
        },

        //画左下
        drawFillLB(rect, w, color) {
            const { x, y, r } = this.fillB(rect, w);
            const x1 = x - r;
            const y1 = y - r;
            this.drawFill(x1, y, x1, y1, r, color);
        },

        //画下右
        drawFillBR(rect, w, color) {
            const { x, y, r } = this.fillR(rect, w);
            const x1 = x - r;
            const y1 = y + r;
            this.drawFill(x, y1, x1, y1, r, color);
        },

        //画右上
        drawFillRT(rect, w, color) {
            const { x, y, r } = this.fillT(rect, w);
            const x1 = x + r;
            const y1 = y + r;
            this.drawFill(x1, y, x1, y1, r, color);
        },
        drawFill(x, y, x1, y1, r, color) {
            this.cxt.arcTo(x, y, x1, y1, r);
            this.cxt.closePath();

            this.cxt.save();
            this.cxt.fillStyle = color;
            this.cxt.fill();
            this.cxt.restore();
        },

        fill(x, y, points, r, w) {
            this.cxt.beginPath();
            this.cxt.moveTo(x, y);
            this.cxt.arcTo(...points, r);
            r = r - w;
            return r;
        },

        fillL({ x, y, x1, y1, r }, w) {
            r = this.fill(x, y, [x1, y, x1, y1], r, w);
            x = x1 + w;
            y = y1;
            this.cxt.lineTo(x, y);
            return { x, y, r };
        },
        fillT({ x, y, x1, y1, r }, w) {
            r = this.fill(x, y, [x, y1, x1, y1], r, w);
            x = x1;
            y = y1 + w;
            this.cxt.lineTo(x, y);
            return { x, y, r };
        },
        fillB({ x, y, x1, y1, r }, w) {
            r = this.fill(x, y, [x, y1, x1, y1], r, w);
            x = x1;
            y = y1 - w;
            this.cxt.lineTo(x, y);
            return { x, y, r };
        },
        fillR({ x, y, x1, y1, r }, w) {
            r = this.fill(x, y, [x1, y, x1, y1], r, w);
            x = x1 - w;
            y = y1;
            this.cxt.lineTo(x, y);
            return { x, y, r };
        },

        //计算并画弧度
        calcDrawArcTo(x, y, r, t, w, color) {
            const rect = this.calcArc[t](x, y, r);
            this.fillALL[t](rect, w, color);
            return { x: rect.x1, y: rect.y1 };
        },
        //画线
        drawLine(x, y) {
            this.cxt.lineTo(x, y);
            return { x, y };
        },
        //画矩形
        drawRect(x, y, x1, y1, w, color) {
            this.cxt.beginPath();
            const ss = new Date().getSeconds();
            const lr = "lr" + (ss % 3);
            const rl = "rl" + ((ss + 1) % 3);
            this.cxt.save();
            let key = lr;
            if (x1 < 0) {
                key = rl;
            }
            this.cxt.fillStyle = color || this.canvasBGImg[key];
            if (x1) {
                y = y - w;
                this.cxt.rect(x, y, x1, w);
                x = x + x1;
            } else {
                x = x - w;
                this.cxt.rect(x, y, w, y + y);
                y = y + y1;
            }
            this.cxt.fill();
            this.cxt.restore();
            return { x, y };
        },
        //画点
        drawPoint({ x, y, color, r, title, d }) {
            this.cxt.beginPath();
            this.cxt.arc(x + r / 3, y + r / 3, r, 0, 2 * Math.PI);

            this.cxt.save();
            this.cxt.fillStyle = color;
            this.cxt.fill();
            if (d === "b") {
                y = y + 2 * r + 20;
                x = x - (r * title.length) / 2;
            }
            if (d === "r") {
                x = x + 2 * r + 10;
                y = y + r;
            }
            this.cxt.font = "30px Georgia";
            this.cxt.fillText(title, x, y);
            this.cxt.restore();
        },
        //画
        draw({
            start,
            radius,
            width,
            notStarted = [],
            notStartedColor,
            color,
            bgcolr,
            path,
            tags = [],
        }) {
            let [x, y] = start;
            this.cxt.moveTo(x, y);

            path.forEach((p) => {
                const { X, Y } = p;
                let point;
                if (X || Y) {
                    point = this.drawRect(x, y, X, Y, width);
                } else if (p === "r") {
                    point = { x: x + width, y };
                } else if (p === "l") {
                    point = { x: x - width, y };
                } else if (p === "b") {
                    point = { x, y: y + width };
                } else if (p === "t") {
                    point = { x, y: y - width };
                } else {
                    point = this.calcDrawArcTo(x, y, radius, p, width, color);
                }
                x = point.x;
                y = point.y;
            });
            this.cxt.beginPath();
            notStarted.forEach((p) => {
                const { X, Y } = p;
                let point;
                if (X || Y) {
                    point = this.drawRect(
                        x,
                        y,
                        X || x,
                        Y || y,
                        width,
                        notStartedColor
                    );
                } else if (p === "r") {
                    point = { x: x + width, y };
                } else if (p === "l") {
                    point = { x: x - width, y };
                } else if (p === "b") {
                    point = { x, y: y + width };
                } else if (p === "t") {
                    point = { x, y: y - width };
                } else {
                    point = this.calcDrawArcTo(
                        x,
                        y,
                        radius,
                        p,
                        width,
                        notStartedColor
                    );
                }
                x = point.x;
                y = point.y;
            });
            tags.forEach((p) => {
                this.drawPoint(p);
            });
        },

        createCanvasImg(img) {
            if (!img) {
                return;
            }
            const canvas = document.createElement("canvas");
            const ctx = canvas.getContext("2d");
            canvas.height = img.height;
            canvas.width = img.width;
            ctx.drawImage(img, 0, 0, img.width, img.height);
            return this.cxt.createPattern(canvas, "repeat");
        },
        //init
        initImg() {
            const leftRight1 = document.getElementById("left-right1");
            const leftRight2 = document.getElementById("left-right2");
            const leftRight3 = document.getElementById("left-right3");

            const rightLeft1 = document.getElementById("right-left1");
            const rightLeft2 = document.getElementById("right-left2");
            const rightLeft3 = document.getElementById("right-left3");
            const lr0 = this.createCanvasImg(leftRight1);
            const lr1 = this.createCanvasImg(leftRight2);
            const lr2 = this.createCanvasImg(leftRight3);
            const rl0 = this.createCanvasImg(rightLeft1);
            const rl1 = this.createCanvasImg(rightLeft2);
            const rl2 = this.createCanvasImg(rightLeft3);
            this.canvasBGImg = {
                lr0,
                lr1,
                lr2,
                rl0,
                rl1,
                rl2,
            };
        },
        startDraw() {
            this.cxt = this.canvas.getContext("2d");
            this.initImg();
            this.cxt.clearRect(0, 0, this.width, this.height);
            console.log(this.width);
            this.cxt.save();
            this.cxt.fillStyle = this.opt.bgcolr;
            this.cxt.fillRect(0, 0, this.width, this.height);
            this.cxt.restore();

            // this.cxt.beginPath();
            // for (let i = 50; i < this.width; i += 50) {
            //     this.cxt.moveTo(i, 0);
            //     this.drawLine(i, this.height);
            // }
            // for (let i = 50; i < this.height; i += 50) {
            //     this.cxt.moveTo(0, i);
            //     this.drawLine(this.width, i);
            // }
            // this.cxt.stroke();
            this.cxt.beginPath();

            this.draw(this.opt);
        },
    },
    mounted() {
        this.canvas = this.$refs.canvas;
        this.$nextTick(() => {
            this.setIntervalStorage = setInterval(this.startDraw, 1000);
        });
    },
    beforeDestroy() {
        clearInterval(this.setIntervalStorage);
    },
};
</script>
<style scoped lang="scss">
.my-canvas {
    height: 100%;
    width: 100%;
    position: relative;
    overflow: hidden;
    .canvas {
        width: 100%;
        &-img {
            display: none;
        }
    }
}
</style>
