<template>
    <div>
        <div class="container">
            <div class="row">
                <span>页数{{rowIndex+1}}/2</span>
            </div>
            <div class="row1">
                    <div
                        class="home-cycle-container"
                        v-for="(item, colIndex) in stateCycle[rowIndex]"
                        :key="colIndex"
                        @click="item.actived ? '' : onCycleClick(colIndex)"
                    >
                        <span>{{stateCycle[rowIndex][colIndex].default}}</span>
                    </div>
            </div>
            <div class="row">
                <button
                    type="button"
                    class="btn btn-default"
                    :disabled="stateButton.default"
                    @click="done ? '' : onButtonClick()"
                >{{done ? '完成(事件为空)' : '下一步'}}</button>
            </div>
        </div>
    </div>
</template>

<script>
import Header from "@/components/home/header";

export default {
    name: "home",
    components: {
        Header
    },
    data: function() {
        return {
            stateCycle: [
                [
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    },
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    },
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    }
                ],
                [
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    },
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    },
                    {
                        default: 1,
                        state1: 2,
                        state2: 3,
                        actived: false
                    }
                ]
            ],

            rowIndex: 0,
            activedNum: 0,
            done: false,

            stateButton: {
                default: true
            }
        };
    },
    methods: {
        onCycleClick: function(colIndex) {
            var randomNum = Math.random() * 10;
            var divider = parseFloat((10 / 2) * 1);
            if (randomNum >= divider) {
                this.stateCycle[this.rowIndex][
                    colIndex
                ].default = this.stateCycle[this.rowIndex][colIndex].state1;
            } else {
                this.stateCycle[this.rowIndex][
                    colIndex
                ].default = this.stateCycle[this.rowIndex][colIndex].state2;
            }

            this.stateCycle[this.rowIndex][colIndex].actived = true;

            this.activedNum = this.activedNum + 1;
            if (this.activedNum === 3) {
                this.stateButton.default = false;
                if (this.rowIndex === 1) {
                    this.done = true;
                }
            }
        },
        onButtonClick: function() {
            this.rowIndex = this.rowIndex + 1;
            this.activedNum = 0;
            this.stateButton.default = true;
        }
    }
};
</script>

<style lang="scss">
.row1 {
    display: flex;
}
.home-cycle-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    height: 100px;
    border-radius: 50px;
    background-image: url(../assets/qq.png);
    background-position: center center;
    background-repeat: no-repeat;
    &:hover {
        cursor: pointer;
    }
}
</style>


