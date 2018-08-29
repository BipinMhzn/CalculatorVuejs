<template>
    <div id="calculator">
        <h1>Simple Calculator</h1>
        <div class="calc">
            <input type="text" class="display result" v-model="display" readonly>
            <input type="button" value="C" class="btnSize operators" v-on:click="clearEntry">
            <input type="button" value="+/-" class="btnSize operators" @click="sign">
            <input type="button" value="%" class="btnSize operators" @click="percent">
            <input type="button" value="/" class="btnSize operators" @click="divide">
            <input type="button" value="7" class="btnSize" @click="appendNum('7')">
            <input type="button" value="8" class="btnSize" @click="appendNum('8')">
            <input type="button" value="9" class="btnSize" @click="appendNum('9')">
            <input type="button" value="*" class="btnSize operators" @click="multiply">
            <input type="button" value="4" class="btnSize" @click="appendNum('4')">
            <input type="button" value="5" class="btnSize" @click="appendNum('5')">
            <input type="button" value="6" class="btnSize" @click="appendNum('6')">
            <input type="button" value="-" class="btnSize operators" @click="subtract">
            <input type="button" value="1" class="btnSize" @click="appendNum('1')">
            <input type="button" value="2" class="btnSize" @click="appendNum('2')">
            <input type="button" value="3" class="btnSize" @click="appendNum('3')">
            <input type="button" value="+" class="btnSize operators" @click="add">
            <input type="button" value="0" class="zero btnSize" @click="appendNum('0')">
            <input type="button" value="." class="btnSize" @click="dot">
            <input type="button" value="=" class="btnSize operators" @click="equalsTo">
       </div>
    </div>    
</template>

<script>
export default {
    name: 'calculator',
    data(){
        return{
            display:'0',
            operator: null,
            previous: null,
            operatorClicked: false
        }
    },
    methods:{
        clearEntry: function(){
            this.display='0';
        },
        appendNum: function(num){
            if(this.operatorClicked){
                this.display='';
                this.operatorClicked=false;
            }
            
            if(this.display==='0')
                this.display = num;
            else
                this.display += num;
        },
        sign:function(){
            if(this.display!='0'){
            if(this.display.charAt(0)==='-')
                this.display=this.display.slice(1);
            else
                this.display='-'+this.display;
            }
        },
        percent: function(){
            this.display=this.display/100;
        },
        dot:function(){
            if(this.display.indexOf('.')===-1)
                this.appendNum('.');
        },
        setPrevious: function(){
            this.previous = this.display;
            this.operatorClicked=true;
        },
        divide:function(){
            this.operator = (a,b) =>a/b;
            this.setPrevious();
        },
        multiply:function(){
            this.operator = (a,b) => a*b;
            this.setPrevious();
        },
        subtract:function(){
            this.operator = (a,b) => b-a;
            this.setPrevious();
        },
        add: function(){
            this.operator = (a,b) => a+b;
            this.setPrevious();
        },
        equalsTo: function(){
            if(this.previous!=null){
                this.display= this.operator(
                    parseFloat(this.display), 
                    parseFloat(this.previous)
                    );
                this.previous=null;  
            }
        }
    }
}
</script>

<style scoped>

.calc{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px,auto);
    margin: 0 auto;
    width: 250px;
}

.display{
    grid-column: 1/5;
    font-size: 150%;
    background-color:navy;
    color: snow;
    text-align: right;
}

.zero{
    grid-column: 1/3;
}

.btnSize{
    font-size: 120%;
    font-style: normal;
    font-weight: bold;
    background-color: aqua;
}

.operators{
    background-color:darkgreen;
    color: antiquewhite;
}

</style>
