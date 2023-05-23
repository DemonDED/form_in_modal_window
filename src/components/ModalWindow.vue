<template>
  <div id="mainForm">
    <div id="headerForm">
      <h1>Title form</h1>
      <p class="closeTab" @click="handle">Close</p>
    </div>
    <div id="bodyForm">
      <div id="inputBodyForm">
        <div v-for="item in placeholders" v-bind:key="item" :class="item">
          <input :placeholder="item" :class="warningCheck"/>
          <p v-show="false" class="warning">{{ 'Pleace fill in ' + item }}</p>
        </div>
      </div>
      <div id="selectProductType">
        <label for="">Product type *</label>
        <select v-model="dataPriceSelect" name="" id="" @change="onChangeSelectedTask">
          <option v-for="item in productTypes" :key="item" :value={item}>{{ 'Product $' + item }}</option>
        </select>
      </div>
      <div id="checkboxForm">
        <div>
          <label for="feat100">Additional feature for 100$</label>
          <label class="checkbox-ios">
            <input type="checkbox" id="feat100" v-model="dataPriceCheckbox1" @change="onChangeChackbox1">
            <span class="checkbox-ios-switch"></span>
          </label>
        </div>
        <div>
          <label for="feat200">Additional feature for 200$</label>
          <label class="checkbox-ios">
            <input type="checkbox" id="feat200" v-model="dataPriceCheckbox2" @change="onChangeChackbox2">
            <span class="checkbox-ios-switch"></span>
          </label>
        </div>
      </div>
      <div id="textareaBodyForm">
        <textarea placeholder="Type your comment" name="" id="" cols="30" rows="10"></textarea>
      </div>
    </div>
    <div id="footerForm">
      <h3>Total price</h3>
      <p>{{'$' + this.dataFullPrice}}</p>
    </div>
    <button @click.prevent="sendForm" id="sendFormBtn">Send form</button>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data() {
    return {
      placeholders: {
        firstName: 'first name *',
        lastName: 'last name *',
        userEmail: 'user@gmail.com *',
      },
      productTypes: {
        firstOption: 50,
        secondOption: 100,
        threeOption: 200,
      },
      warningCheck: false,
      dataPriceSelect: 50,
      dataPriceCheckbox1: null,
      dataPriceCheckbox2: null,
      dataFullPrice: 0,
    }
  },
  methods: {
    sendForm() {
      // console.log(this.dataPriceSelect + this.dataPriceCheckbox1 + this.dataPriceCheckbox2);
      if (this.dataPriceCheckbox1) {this.dataPriceCheckbox1 = 100} else {this.dataPriceCheckbox1 = 0}
      if (this.dataPriceCheckbox2) {this.dataPriceCheckbox2 = 200} else {this.dataPriceCheckbox2 = 0}
      this.dataFullPrice = this.dataPriceSelect.item + this.dataPriceCheckbox1 + this.dataPriceCheckbox2
      console.log(this.dataPriceSelect.item + this.dataPriceCheckbox1 + this.dataPriceCheckbox2)
    },
    onChangeSelectedTask() {
      this.dataFullPrice = this.dataPriceSelect.item;
    },
    onChangeChackbox1() {
      if (this.dataPriceCheckbox1) {this.dataFullPrice += 100} else {this.dataFullPrice -= 100}
    },
    onChangeChackbox2() {
      if (this.dataPriceCheckbox2) {this.dataFullPrice += 200} else {this.dataFullPrice -= 200}
    },
    handle() {
      this.$emit('show')
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #mainForm > * {
    box-sizing: border-box;
  }
  #mainForm {
    width: 40%;
    padding: 1rem;
    margin: auto;
    box-shadow: 0px 0px 2px 1px  black;
  }
  #headerForm, #selectProductType, #checkboxForm > div, #footerForm {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    
  }
  #bodyForm {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #inputBodyForm > * {
    width: 100%;
  }
  #inputBodyForm > *, #selectProductType > *, #checkboxForm > * {
    margin-bottom: 2rem;
  }
  #checkboxForm {
    width: 100%;
  }


  .closeTab {
    cursor: pointer;
  }







  .checkbox-ios {
	display: inline-block;    
	height: 28px;    
	line-height: 28px;  
	margin-right: 10px;      
	position: relative;
	vertical-align: middle;
	font-size: 14px;
	user-select: none;	
}
.checkbox-ios .checkbox-ios-switch {
	position: relative;	
	display: inline-block;
	box-sizing: border-box;			
	width: 56px;	
	height: 28px;
	border: 1px solid rgba(0, 0, 0, .1);
	border-radius: 25%/50%;	
	vertical-align: top;
	background: #eee;
	transition: .2s;
}
.checkbox-ios .checkbox-ios-switch:before {
	content: '';
	position: absolute;
	top: 1px;
	left: 1px;	
	display: inline-block;
	width: 24px;	
	height: 24px;
	border-radius: 50%;
	background: white;
	box-shadow: 0 3px 5px rgba(0, 0, 0, .3);
	transition: .15s;
}
.checkbox-ios input[type=checkbox] {
	display: block;	
	width: 0;
	height: 0;	
	position: absolute;
	z-index: -1;
	opacity: 0;
}
.checkbox-ios input[type=checkbox]:not(:disabled):active + .checkbox-ios-switch:before {
	box-shadow: inset 0 0 2px rgba(0, 0, 0, .3);
}
.checkbox-ios input[type=checkbox]:checked + .checkbox-ios-switch {
	background: limegreen;
}
.checkbox-ios input[type=checkbox]:checked + .checkbox-ios-switch:before {
	transform:translateX(28px);
}
 
/* Hover */
.checkbox-ios input[type="checkbox"]:not(:disabled) + .checkbox-ios-switch {
	cursor: pointer;
	border-color: rgba(0, 0, 0, .3);
}
 
/* Disabled */
.checkbox-ios input[type=checkbox]:disabled + .checkbox-ios-switch {
	filter: grayscale(70%);
	border-color: rgba(0, 0, 0, .1);
}
.checkbox-ios input[type=checkbox]:disabled + .checkbox-ios-switch:before {
	background: #eee;
}
 
/* Focus */
.checkbox-ios.focused .checkbox-ios-switch:before {
	box-shadow: inset 0px 0px 4px #ff5623;
}


  .warning {
    display: flex;
    justify-self: flex-start;
    color: red;
    font-size: 0.8rem;
  }
  #inputBodyForm {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  #inputBodyForm > div > input {
    width: 100%;
    height: 2.5rem;
    border: 1px solid gray;
    border-radius: 0.2rem;
  }

  select {
    width: 50%;
    height: 2.5rem;
  }
  #textareaBodyForm {
    width: 100%;
  }
  textarea {
    width: 100%;
  }

  #sendFormBtn {
    width: 10rem;
    height: 3rem;
    border: none;
    color: white;
    background-color: rgb(54, 54, 255);
    cursor: pointer;
    border-radius: 1rem;
    font-size: 1.3rem;
  }
</style>
