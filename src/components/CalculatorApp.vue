<template>

<div class=" w-[400px] max-[410px]:w-[90%] mx-auto border border-blue-100 shadow-md p-2">
    <h1 class="p-5 text-lg font-semibold">Simple Calculator</h1>
    <input v-model="display" @keydown="handleKeyDown" readonly type="text" class="border focus:outline-blue-300 border-gray-300 p-2 w-full" :class="dynamicClass">

    <div class="grid grid-cols-4 grid-rows-4 gap-y-2 max-[410px]:gap-x-2 p-4 ">
        <button @click="appendToDisplay('7')"  class="inline-block min-[410px]:py-4 min-[410px]:px-8  hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">7</button>
        <button @click="appendToDisplay('8')"  class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">8</button>
        <button @click="appendToDisplay('9')"  class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">9</button>
        <button @click="appendToDisplay('/')"  class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-yellow-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">/</button>
        
        <button @click="appendToDisplay('4')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">4</button>
        <button @click="appendToDisplay('5')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">5</button>
        <button @click="appendToDisplay('6')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">6</button>
        <button @click="appendToDisplay('*')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-yellow-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">*</button>
        
        <button @click="appendToDisplay('1')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">1</button>
        <button @click="appendToDisplay('2')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">2</button>
        <button @click="appendToDisplay('3')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">3</button>
        <button @click="appendToDisplay('-')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-yellow-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">-</button>
        
        <button @click="appendToDisplay('0')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">0</button>
        <button @click="appendToDisplay('.')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-blue-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">.</button>
        <button @click="calculate" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-green-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400">=</button>
        <button @click="appendToDisplay('+')" class="inline-block min-[410px]:py-4 min-[410px]:px-8 hover:bg-yellow-400 hover:text-white hover:font-bold bg-gray-200 w-max py-3 px-6 mx-auto rounded shadow-md border border-gray-400 ">+</button>
           
     </div>
     <div class="flex justify-between space-x-1">
        <button @click="clearDisplay" class=" flex-1 bg-gray-200 hover:bg-red-400 hover:text-white hover:font-bold py-3 px-6  rounded shadow-md border border-gray-400">C</button>
        <button @click="removeNumber" class=" flex-1 bg-gray-200 hover:bg-red-400 hover:text-white hover:font-bold py-3 px-6  rounded shadow-md border border-gray-400">Backspace</button>
     </div>
     
</div>




</template>

<script setup>
import {ref, computed} from "vue";

const display= ref('0')

const appendToDisplay = (value) => {
    if (value ==='.' &&  display.value.includes('.')) {
        return; //it means it will do nothing if there is a decimal already.
    } 
    else if (display.value === '0' && value !== '.') { 
        display.value = value //so if we enter 7, 0 will be replaced with 7. but if we enter decimal it will become 0. (concatenates)
    } else { 
        display.value += value //this concatenates it because it is a string. say the value is 7, and we add 7, result: 77
        //if display.value is zero and value is zero too, it won't be added. but rather the second condition will be true and zero will be replaced with zero
    }
}

const handleKeyDown = (event) => { //this function enables the use of number keys on the keyboard
    const key = event.key

    if (!isNaN(key) && key !== '') { //if it is a number and not null
        appendToDisplay(key)
    }else if (key === '.' || key === ','){ //if it is . or , add .
        appendToDisplay('.')
    } else if (key === '*' || key === '/' || key === '+' || key === '-' ) { //for special characters, since they are not numbers so won't pass the first if logic
        appendToDisplay(key)
    } else if (key === '=' || key === 'Enter') { //same thing as above
        calculate()
    } else if (key === 'Backspace') { //removing a number using removeNumber function
        removeNumber()
    }
}

const removeNumber = () => {
    
     if (display.value.length > 1) { //if more than 2 numbers, remove the last
        display.value = display.value.slice (0, -1)
    } else if (display.value.length === 1) {
        display.value = '0' // if only one number, replace it with 0. this prevents backspacing to null, if the length is 1, whategver number, backspacing will reset it to 0
    }
}

const calculate = () => {
    try {
        display.value = eval(display.value).toString(); //eval is a method that is used to execute code that is in a form of string. here our code is string. so if we enter "7 * 7" it will treat it as 7 * 7. and we use toString to turn the result back to a string in order to concatenate it with any new numbers
    }

    catch(error) {
        display.value = "Error"
    }
}

const clearDisplay = () => {
    display.value = '0'
}

const dynamicClass = computed(() => {
    return display.value.length > 20 ?  'text-sm' : ''
    //this is a terinary coniditon, if our number length is big, we give it a small text style. so here we do class binding to a function rather than a property. and that function should return someting for the class.
}
)

</script>