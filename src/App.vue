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
                start: [209, 35],
                radius: 25,
                bgcolor: "#1226BF",
                width: 16,
                color: "#55cc7c",
                defaultColor: "#d9d9d9",
                path: [
                    {
                        color: "#ffd200",
                        r: 23,
                        title: "配页",
                        isDefault: true,
                        d: "b",
                    },
                    { X: 831 },
                    {
                        color: "#17ff37",
                        r: 23,
                        title: "胶装",
                        d: "b",
                    },
                    { X: 478 },
                    "tr",
                    "rb",
                    't',
                    { X: -410 },
                    "tl",
                    "lb",
                    't',
                    { X: 410 },
                    {
                        color: "#17ff37",
                        r: 23,
                        title: "称重检测",
                        d: "r",
                    },
                    "tr",
                    "rb",
                    't',
                    { X: -110 },
                    {
                        color: "#ff5c03",
                        r: 23,
                        title: "裁切",
                        isDefault: true,
                        d: "b",
                    },
                    { X: -245 },
                    {
                        color: "#ff5c03",
                        r: 23,
                        title: "分本堆积",
                        isDefault: true,
                        d: "b",
                    },
                    { X: -180 },
                    "tl",
                    "r",
                    "rb",
                    't',
                    { X: -60 },
                    {
                        color: "#17ff37",
                        r: 23,
                        title: "质检台",
                        d: "b",
                    },
                    { X: -70 },
                    "b",
                    "bl",
                    "r",
                    "rt",
                    { X: -110 },
                    {
                        color: "#ff5c03",
                        r: 23,
                        title: "打捆",
                        isDefault: true,
                        d: "b",
                    },
                    { X: -250 },
                    {
                        color: "#ffd200",
                        r: 23,
                        title: "机器码垛",
                        d: "b",
                    },
                ],
                tags: [
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
