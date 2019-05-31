<template>
    <div id="app" class="h-100" @contextmenu.prevent="">
        <div class="container-fluid h-100 calculator">
            <div class="row bg-gray p-5 text-light justify-content-around">
                <span class="result">{{this.total}}</span>
                <span class="result">{{this.symbol ? this.symbol:''}}</span>
                <span class="result">{{this.second ? this.second: '0'}}</span>
            </div>
            <div class="row">
                <button type="button" class="btn btn-secondary col-6" @click="resetAll()">AC</button>
                <button type="button" class="btn btn-secondary col-3" @click="setMinus()">+/-</button>
                <button type="button" class="btn btn-warning text-light col-3" @click="clickSymbols('÷')">÷</button>
            </div>
            <div class="row">
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('7')">7</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('8')">8</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('9')">9</button>
                <button type="button" class="btn btn-warning text-light col-3" @click="clickSymbols('*')">*</button>
            </div>
            <div class="row">
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('4')">4</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('5')">5</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('6')">6</button>
                <button type="button" class="btn btn-warning text-light col-3" @click="clickSymbols('-')">-</button>
            </div>
            <div class="row">
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('1')">1</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('2')">2</button>
                <button type="button" class="btn btn-secondary col-3" @click="clickNums('3')">3</button>
                <button type="button" class="btn btn-warning text-light col-3" @click="clickSymbols('+')">+</button>
            </div>
            <div class="row">
                <button type="button" class="btn btn-secondary col-6" @click="clickNums(0)">0</button>
                <button type="button" class="btn btn-secondary col-3"@click="clickNums('.')">.</button>
                <button type="button" class="btn btn-warning text-light col-3" @click="calculateResult()">=</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'App',
        data() {
            return {
                total: 0,
                symbol:false,
                second:false
            }
        },
        calculated:{
            total(){

            }
        },
        methods:{
            clickNums(num){
                if(this.total){
                    this.total = this.total + num
                }else if(num === '.'){
                    this.total = this.total + num
                }else{
                    this.total = num
                }
            },
            clickSymbols(symbol){
                if(this.total && this.second){
                    this.calculateResult();
                }else if(this.total){
                    this.second = this.total;
                    this.total = 0;
                }
                this.symbol = symbol;
            },
            resetAll(){
                this.symbol = false;
                this.second = false;
                this.total = 0;
            },
            setMinus(){
                this.total = -this.total;
            },
            calculateResult(){
                let sym = this.symbol;
                switch(sym){
                    case '+' :
                        this.total = +this.second + +this.total;
                        break;
                    case '-' :
                        this.total = this.second - this.total;
                        break;
                    case '*' :
                        this.total = this.second * this.total;
                        break;
                    case '÷' :
                        this.total = this.second / this.total;
                        break;
                }
                this.second = this.total;
                this.total = 0;
            }
        }
    }
</script>
<style>
    body{
        height: 100vh;
    }
    .calculator>.row {
        height: 16.66%;
    }
    .bg-gray {
        background: #858694;
    }
    .btn:not(:disabled):not(.disabled) {
        cursor: pointer;
    }
    .result {
        font-size: 48px;
        font-weight: 600;
    }
    .text-light {
        color: #f8f9fa!important;
    }
    .btn-secondary {
        background: #e0e0e0;
        color: #000;
    }
    .btn {
        border-radius: 0;
        border: 0px;
        border-top: 1px solid;
        border-right: 1px solid;
        font-size: 48px;
        font-weight: 600;
        cursor: pointer !important;
    }
    .btn-warning {
        background: #f5923e;
        border-color: #000;
    }
    .btn-warning:hover, .btn-warning:focus {
        background: #ffa961;
        color: #fff;
        border-color: #000;
    }
    .btn-secondary:hover, .btn-secondary:focus {
        background: #ccc;
        color: #000;
    }
</style>

