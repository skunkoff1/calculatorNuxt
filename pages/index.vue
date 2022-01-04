<template>
  <div id="container">
    <div id="calc">
      <div id="screenarea">
        <div id="screen">
          <div>
            <p>{{number1}}</p>
          </div>
          <div>
            <p>{{operator}}</p>
          </div>
          <div>
            <p>{{number2}}</p>
          </div>
        </div>
        <div id="result">
          <p>{{result}}</p>
        </div>

      </div>
      <div id="keyboard">
        <div class="row1">
          <button class="button" @click="eraseAll()"><p>Ce</p></button>
          <button class="button" @click="eraseCurrent()"><p>C</p></button>
          <button class="button" @click="erase()"><p>&larr;</p></button>
          <button class="button" @click="plusMinus()"><p>&plusmn;</p></button>
        </div>
        <div class="row2">
          <button type="button" class="button" @click="input(7)"><p>7</p></button>
          <button type="button" class="button" @click="input(8)"><p>8</p></button>
          <button type="button" class="button" @click="input(9)"><p>9</p></button>
          <button type="button" class="button" @click="operate('/')"><p>/</p></button>
        </div>
        <div class="row2">
          <button type="button" class="button" @click="input(4)"><p>4</p></button>
          <button type="button" class="button" @click="input(5)"><p>5</p></button>
          <button type="button" class="button" @click="input(6)"><p>6</p></button>
          <button type="button" class="button" @click="operate('*')"><p>X</p></button>
        </div>
        <div class="row2">
          <button type="button" class="button" @click="input(1)"><p>1</p></button>
          <button type="button" class="button" @click="input(2)"><p>2</p></button>
          <button type="button" class="button" @click="input(3)"><p>3</p></button>
          <button type="button" class="button" @click="operate('-')"><p>-</p></button>
        </div>
        <div class="row2">
          <button type="button" class="button" @click="input('.')"><p>.</p></button>
          <button type="button" class="button" @click="input(0)"><p>0</p></button>
          <button type="button" class="button" @click="calculate()"><p>=</p></button>
          <button type="button" class="button" @click="operate('+')"><p>+</p></button>
        </div>
      </div>
    <div id="message" v-if="message!=''">
      <p>{{message}}</p>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
    isCalcul: false,
    number1: "",
    number2:"",
    result:'',
    operator:"",
    isDot: false,
    message:'',
    minus: false
    }
  },
  methods: {
     input(x) {
       if(this.isCalcul == true) {
         this.number1 = ''
         this.number2=''
         this.operator=''
         this.result=''
         this.isCalcul = false
       }
       if(this.operator == '') {
         if(x == '.' && this.isDot == false) {
           this.isDot = true
            return this.number1+=x
         }
         else if(x == '.' && this.isDot == true) {
           return this.number1
         }
         return this.number1+=x
       }
       else {
         if(x == '.' && this.isDot == false) {
           this.isDot = true
            return this.number2+=x
         }
         else if(x == '.' && this.isDot == true) {
           return this.number2
         }
         return this.number2+=x
       }
    return this.number1+=x
    },
    operate(x) {
      this.isDot=false;
      this.operator+=x
    },
    calculate() {
      this.number1 = Number(this.number1)
      this.number2 = Number(this.number2)
      switch(this.operator) {
        case '+':
          this.result = this.number1 + this.number2
          break;
          case '-':
          this.result = this.number1 - this.number2
          break;
          case '*':
          this.result = this.number1 * this.number2
          break;
          case '/':
            if(this.number2 == 0) {
              return this.message = "division par zéro impossible"
            }
          this.result = this.number1 / this.number2
          break;
      }
        this.isCalcul = true
        this.isDot = false
        this.minus = false
        return this.screen2 = this.result
  },
    erase() {
      if(this.operator =='') {
        this.number1= this.number1.slice(0,this.number1.length-1)
      }
      else {
        this.number2=  this.number2.slice(0,this.number2.length-1)
      }

    },
    eraseAll() {
      this.number1=''
      this.number2=''
      this.result=''
      this.operator =''
    },
    eraseCurrent() {
      if(this.operator =='') {
        this.number1=''
      }
      else {
        this.number2=''
      }

    },
    plusMinus() {
      if(this.operator == '') {
        if(this.number1[0]== '-') {
          this.number1= this.number1.slice(1, this.number1.length)
        }
        else {
          this.number1 = "-" + this.number1
        }
      }
      else {
        if(this.number2[0]== '-') {
          this.number2= this.number2.slice(1, this.number2.length)
        }
        else {
          this.number2 = "-" + this.number2
        }
      }
    }
  }
}
</script>

<style>
textarea{
  text-align:right;
  font-size: 25px;
  margin:-5px;
  border: none;
}
#calc {
  width:500px;
  background-color: rgb(51, 50, 50);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding:20px;
}

#message {
  background-color: red;
  border-radius: 5px;
}

#container {
  width:1200px;
  margin:auto;
}

#screen {
  display: flex;
}

#result {
  display: flex;
  justify-content: flex-end;
}

#screenarea {
  margin:25px;
  background-color: white;
  width:450px;
  height: 200px;
  display: flex;
  flex-direction: column;
}

.row1, .row2 {
  display: flex;
}

.button {
  width:60px;
  height:60px;
  margin:5px;
  background-color: darkgray;
  display: flex;
  justify-content: center;
  align-items: center;
  border:none;
}

button:hover {
  filter: brightness(0.8);
}

button:active {
 -webkit-box-shadow: inset -1px 3px 8px 5px #272829, 2px 5px 16px 0px rgb(44, 44, 44), 0px 0px 50px -30px rgba(31,30,30,0);
box-shadow: inset -1px 3px 8px 5px #272829, 2px 5px 16px 0px rgb(44, 44, 44), 0px 0px 50px -30px rgba(31, 30, 30, 0);
}

p {
  padding-top: 12px;
  font-size: 30px;
}
</style>
