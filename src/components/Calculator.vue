<template>
    <div class="calculator">
        <!--<div class="display">{{ viewfinder() }}</div>-->
        <div class="display">{{ result || "0" }}</div>
        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn">+/-</div>
        <div @click="percent" class="btn">%</div>
        <div @click="division" class="btn operator">÷</div>
        <div @click="digit('7')" class="btn">7</div>
        <div @click="digit('8')" class="btn">8</div>
        <div @click="digit('9')" class="btn">9</div>
        <div @click="times" class="btn operator">x</div>
        <div @click="digit('4')" class="btn">4</div>
        <div @click="digit('5')" class="btn">5</div>
        <div @click="digit('6')" class="btn">6</div>
        <div @click="minus" class="btn operator">-</div>
        <div @click="digit('1')" class="btn">1</div>
        <div @click="digit('2')" class="btn">2</div>
        <div @click="digit('3')" class="btn">3</div>
        <div @click="sum" class="btn operator">+</div>
        <div @click="digit('0')" class="btn zero">0</div>
        <div @click="point" class="btn">.</div>
        <div @click="equal" class="btn operator">=</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            prior: null,
            result: "",
            operatorClicked: false,
            operator: null,
        };
    },

    methods: {
        clear() {
            this.result = "";
        },

        sign() {
            this.result =
                this.result.charAt(0) === "-"
                    ? this.result.slice(1)
                    : `-${this.result}`;
        },

        percent() {
            this.result = `${parseFloat(this.result) / 100}`;
        },

        digit(number) {
            if (this.operatorClicked) {
                this.result = "";
                this.operatorClicked = false;
            }
            this.result = `${this.result}${number}`;
        },

        point() {
            if (this.result.indexOf(".") === -1) {
                this.digit(".");
            }
        },

        setPrior() {
            this.prior = this.result;
            this.operatorClicked = true;
        },

        division() {
            this.operator = (x, y) => x / y;
            this.setPrior();
        },

        times() {
            this.operator = (x, y) => x * y;
            this.setPrior();
        },

        minus() {
            this.operator = (x, y) => x - y;
            this.setPrior();
        },

        sum() {
            this.operator = (x, y) => x + y;
            this.setPrior();
        },

        equal() {
            this.result = `${this.operator(
                parseFloat(this.prior),
                parseFloat(this.result)
            )}`;
            this.prior = null;
        },

        /*viewfinder() {
            const num1 = this.prior
            const num2 = this.result
            console.log(this.operator)
            return(`${num1} ${num2}`)
        }*/
    },
};
</script>

<style scoped>
.calculator {
    display: grid;
    font-size: 30px;
    grid-auto-rows: minmax(50px, auto);
    grid-template-columns: repeat(4, 1fr);
    margin: 0 auto;
    width: 400px;
}

.display {
    grid-column: 1 / 5;
    background-color: #546a7b;
    padding-left: 10px;
}

.zero {
    grid-column: 1 / 3;
}

.btn {
    background-color: #9ea3b0;
    border: 1px solid #0d1f2d;
}

.operator {
    background-color: #e4c3ad;
}

@media screen and (max-width: 390px) {
    .calculator {
    display: grid;
    font-size: 30px;
    grid-auto-rows: minmax(50px, auto);
    grid-template-columns: repeat(4, 1fr);
    margin: 0 auto;
    width: 100%;
}
}
</style>
