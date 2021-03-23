<template>
    <div id="app">
        <MyCanvas :opt="opt">
            <img height="17" id="left-right1" src="./assets/01-L.png" />
            <img height="17" id="left-right2" src="./assets/01-C.png" />
            <img height="17" id="left-right3" src="./assets/01-R.png" />
            <img height="17" id="right-left1" src="./assets/02-R.png" />
            <img height="17" id="right-left2" src="./assets/02-C.png" />
            <img height="17" id="right-left3" src="./assets/02-L.png" />
        </MyCanvas>
    </div>
</template>
<script>
import MyCanvas from "@/components/canvas.vue";

export default {
    components: {
        MyCanvas,
    },
    data() {
        return {
            opt: {
                start: [209, 51],
                radius: 25,
                bgcolor: "#1226BF",
                width: 16,
                color: "#55cc7c",
                notStartedColor: "#d9d9d9",
                path: [
                    { X: 1309 },
                    "tr",
                    "rb",
                    { X: -410 },
                    "tl",
                    "lb",
                    { X: 410 },
                    "tr",
                    "rb",
                    { X: -450 },
                    "tl",
                    "r",
                    "rb",
                    { X: -50 },
                ],
                tags: [
                    {
                        x: 184,
                        y: 37,
                        color: "#17ff37",
                        r: 23,
                        title: "配页",
                        d: "b",
                    },
                    {
                        x: 831,
                        y: 37,
                        color: "#17ff37",
                        r: 23,
                        title: "胶装",
                        d: "b",
                    },
                    {
                        x: 1530,
                        y: 110,
                        color: "#17ff37",
                        r: 23,
                        title: "称重检测",
                        d: "r",
                    },
                    {
                        x: 1412,
                        y: 143,
                        color: "#17ff37",
                        r: 23,
                        title: "裁切",
                        d: "b",
                    },
                    {
                        x: 1170,
                        y: 143,
                        color: "#17ff37",
                        r: 23,
                        title: "分本堆积",
                        d: "b",
                    },
                    {
                        x: 973,
                        y: 180,
                        color: "#17ff37",
                        r: 23,
                        title: "质检台",
                        d: "b",
                    },
                    {
                        x: 753,
                        y: 143,
                        color: "#ff5c03",
                        r: 23,
                        title: "打捆",
                        d: "b",
                    },
                    {
                        x: 472,
                        y: 143,
                        color: "#ffd200",
                        r: 23,
                        title: "机器码垛",
                        d: "b",
                    },
                    {
                        x: 20,
                        y: 113,
                        color: "#17ff37",
                        r: 13,
                        title: "运行",
                        d: "r",
                    },
                    {
                        x: 20,
                        y: 163,
                        color: "#ffd200",
                        r: 13,
                        title: "待机",
                        d: "r",
                    },
                    {
                        x: 20,
                        y: 210,
                        color: "#ff5c03",
                        r: 13,
                        title: "报警",
                        d: "r",
                    },
                ],
                notStarted: [
                    "b",
                    { X: -80 },
                    "b",
                    "bl",
                    "r",
                    "rt",
                    "b",
                    { X: -379 },
                ],
            },
        };
    },
};
</script>
<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
</style>
