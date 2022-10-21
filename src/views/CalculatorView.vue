<template>
  <div class="calculation">
    <!-- <div class="inp">{{ process.count }}</div> -->
    <!-- <input class="inp" type="text" disabled :value="process.count" @keyup="value=value.replace(/[^\d\.\+\/\*\-\%]/g,''),vuas($event)"> -->
    <input class="inp" type="text" :value="process.count.toLocaleString()" onkeyup="value=value.replace(/[^\d\.\+\/\*\-\%]/g,''),vuas($event)">
    <div class="btn">
      <button v-for="item in buttonArr" :key="item.id" @click="assign($event,item)">{{ item }}</button>
      <!-- <button @click="empty">AC</button>
      <button @click="del">删除</button>
      <button>+/-</button>
      <button @click="except">÷</button>
      <button @click="seven">7</button>
      <button @click="eight">8</button>
      <button @click="nine">9</button>
      <button @click="ride">*</button>
      <button @click="four">4</button>
      <button @click="five">5</button>
      <button @click="six">6</button>
      <button @click="reduce">-</button>
      <button @click="one">1</button>
      <button @click="two">2</button>
      <button @click="three">3</button>
      <button @click="add">+</button>
      <button @click="zero" class="zero">0</button> 
      <button @click="spot">.</button>
      <button>=</button> -->
    </div>
  </div>
</template>

<script setup>
import { reactive,computed, onMounted } from 'vue';

// const showInfo = (e) => {
//   console.log(e.target.value)  //打印出来的是输入框里面的内容 
// }

let process = reactive({
  count:""
})
const buttonArr = [
  "AC", "back", "%", "+", "7", "8", "9", "-", "4", "5", "6", "*", "1", "2", "3", "/", ".", "0", "="
]

const assign = (event,item) => {
  switch(item){
    case "0":
    checkZero(event)
    break;
    case "1":
    case "2":
    case "3":
    case "4":
    case "5":
    case "6":
    case "7":
    case "8":
    case "9":
    checkNum(event, item)
    break;
    case "AC":
      clear()
    break;
    case "back":
      back()
    break;
    case "+":
    case "-":
    case "/":
    case "*":
    case ".":
      checkOperator(event, item);
    break;
    case "=":
      calculate();
    break;
    case "%":
      turnFloat()
    break;
    default:
    process.count += item
  }
}
const lastChar = computed(() => {
      return process.count.charAt(process.count.length - 1);
    })
const deleteLastChar = () => {
      //删除最后一位字符
      return process.count.substring(0, process.count.length - 1);
    }
const back = () =>{
      //back,删除算式的最后一位
      process.count == ""
        ? clear()
        : (process.count = deleteLastChar()); //当删到算式为空时,调用clear(),相当于按了一次'C'键 : 如果算式不为空,则删掉其最后一位的字符
    }
const clear = () => {
      //AC,清空保存算式和结果的属性
      process.count  = "";
    }
const checkZero = (event) => {
      //0
      process.count == "0"
      ? event.preventDefault()
      : (process.count += "0"); //如果算式只有一个0,则阻止本次操作
}
const checkNum =(event, item) => {
      //对应1-9键
    process.count == "0"
      ? ((process.count = ""), (process.count += item))
      : (process.count += item); //如果当前算式只有一个0,则删除这个0再将数字拼入算式
}
const checkOperator = (event, item) => {
      //对应+-*/.键
      let reg = /-|[/]|[+]/
      if (item === "-") {
        return (process.count += item);
      }
      if (!reg.test(lastChar)) {
        //如果算式最后一位已经是运算符或算式为空且点击的键不是-,则阻止本次操作
        process.count += item;
      }
    }
    
const calculate= () => {
  //求和
  // parseFloat((0.1 + 0.2).toFixed(10))
 process.count = parseFloat(eval(process.count).toFixed(10) + "");
// console.log(process.count.)

} 

const turnFloat = () => {
  // %
  process.count = process.count*0.01.toString();
}
const vuas = (event) => {
  window.addEventListener('keyup', vuas)
  console.log("键盘按下了",event.key)
  console.log("键盘按下了",event)
  // let zhi = event.key 
  // process.count += zhi
}
onMounted(() =>{
  window.addEventListener('keyup', vuas)
})

// const zero = () => {
//   process.count += "0"
// }
// const one = () => {
//   process.count += "1"
// }
// const two = () => {
//   process.count += "2"
// }
// const three = () => {
//   process.count += "3"
// }
// const four = () => {
//   process.count += "4"
// }
// const five = () => {
//   process.count += "5"
// }
// const six = () => {
//   process.count += "6"
// }
// const seven = () => {
//   process.count += "7"
// }
// const eight = () => {
//   process.count += "8"
// }
// const nine = () => {
//   process.count += "9"
// }
// const reduce = () => {
//   process.count += "-"
// }
// const add = () => {
//   process.count += "+"
// }
// const ride = () => {
//   process.count += "*"
// }
// const except = () => {
//   process.count += "÷"
// }
// // 清空
// const empty = () => {
//   process.count = ""
// }
// const spot = () => {
//   process.count += "."
// }
// // 删除
// const del = () => {
    
// }
</script>

<style >
.calculation {
  display: flex;
  width: 400px;
  flex-wrap: wrap;
  justify-content: center;
  margin-left: 50%;
  transform: translate(-50%);
  box-shadow: #ccc 0px 0px 10px;
  border-radius: 10px;
}

.inp {
  width: 340px;
  height: 50px;
  line-height: 50px;
  text-align: right;
  padding-right: 20px;
  margin: 20px 0 10px 0;
  font-size: 30px;
  border-radius: 40px;
  background-color: #f7f7f7;
  overflow: hidden;
  border: 0;
  outline: none;
}

.btn button {
  width: 80px;
  height: 50px;
  border-radius: 50px;
  margin: 6px;
  border: 0;
}

.btn {
  margin-bottom: 20px;
}

.btn button.zero {
  width: 172px;
}
.btn :last-child{
  width: 172px;
}
</style>
