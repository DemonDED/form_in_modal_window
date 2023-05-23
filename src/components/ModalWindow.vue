<template>
  <div id="mainForm">
    <div id="headerForm">
      <h1>Title form</h1>
      <p class="closeTab" @click="handle">X</p>
    </div>
    <div id="bodyForm">
      <div id="inputBodyForm">
        <div>
          <input class="def" placeholder="First Name *" v-model="first_name" @change="onChangeInputFirst" @blur="isFirstNameTouched = true" :class="{ error: isInputFirstNameEmpty, error: sendCheckFirst}" /> 
          <p v-if="isInputFirstNameEmpty || sendCheckFirst" class="warning">Please fill in first name.</p>
        </div>
        <div>
          <input class="def" placeholder="Last Name *" v-model="last_name" @change="onChangeInputLast" @blur="isLastNameTouched = true" :class="{ error: isInputLastNameEmpty, error: sendCheckLast}" /> 
          <p v-if="isInputLastNameEmpty || sendCheckLast" class="warning">Please fill in last name.</p>
        </div>
        <div>
          <input class="def" placeholder="user@gmail.com *" v-model="email" @change="onChangeInputEmail" @blur="isEmailTouched = true" :class="{ error: isEmailError, error: isInputUserEmailEmpty, error: sendCheckEmail}" /> 
          <p v-if="isEmailError" class="warning">Please enter a valid email address.</p>
          <p v-if="isInputUserEmailEmpty || sendCheckEmail" class="warning">Please fill in email.</p>
        </div>
      </div>
      <div id="selectProductType">
        <label for="">Product type *</label>
        <div>
          <select v-model="dataPriceSelect" name="" id="" @change="onChangeSelectedTask" :class="{ error: sendCheck}">
            <option v-for="item in productTypes" :key="item" :value={item}>{{ 'Product $' + item }}</option>
          </select>
          <p v-if="sendCheck" class="warning">Please select product type.</p>
        </div>
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
        <textarea v-model="textArea" placeholder="Type your comment" name="" id="" cols="30" rows="10"></textarea>
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
const emailCheckedRegex = /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/;

export default {
  name: 'HelloWorld',
  data() {
    return {
      email: null,
      isEmailTouched: false,
      last_name: null,
      isLastNameTouched: false,
      first_name: null,
      isFirstNameTouched: false,

      productTypes: {
        firstOption: 50,
        secondOption: 100,
        threeOption: 200,
      },

      textArea: null,
      dataPriceSelect: 50,
      dataPriceCheckbox1: null,
      dataPriceCheckbox2: null,
      dataFullPrice: 0,
      sendCheck: false,
      sendCheckFirst: false,
      sendCheckLast: false,
      sendCheckEmail: false,
    }
  },
  methods: {
    sendForm() {
      if (this.first_name && this.last_name && emailCheckedRegex.test(this.email) && this.dataPriceSelect) {
        const sendObj = {
          firstName: this.first_name,
          lastName: this.last_name,
          email: this.email,
          productType: this.dataPriceSelect.item,
          addFeatFor100: this.dataPriceCheckbox1,
          addFeatFor200: this.dataPriceCheckbox2,
          tetxtAreaData: this.textArea,
          totalPrice: this.dataFullPrice,
        }
        console.log(sendObj);
      } else {
        this.onChangeInputFirst();
        this.onChangeInputLast();
        this.onChangeInputEmail();
        this.onChangeSelectedTask();

        return false;
      }
    },
    onChangeSelectedTask() {
      if (!this.dataPriceSelect.item) {
        this.sendCheck = true;
      } else {
        this.sendCheck = false;
      }
      this.dataFullPrice = this.dataPriceSelect.item;
    },
    onChangeChackbox1() {
      if (this.dataPriceCheckbox1) {this.dataFullPrice += 100} else {this.dataFullPrice -= 100}
    },
    onChangeChackbox2() {
      if (this.dataPriceCheckbox2) {this.dataFullPrice += 200} else {this.dataFullPrice -= 200}
    },
    onChangeInputFirst() {
      if (!this.first_name) {
        this.sendCheckFirst = true;
      } else {
        this.sendCheckFirst = false;
      }
    },
    onChangeInputLast() {
      if (!this.last_name) {
        this.sendCheckLast = true;
      } else {
        this.sendCheckLast = false;
      }
    },
    onChangeInputEmail() {
      if (!this.email) {
        this.sendCheckEmail = true;
      } else {
        this.sendCheckEmail = false;
      }
    },
    handle() {
      this.$emit('show')
    }
  },
  computed: {
    isEmailValid() {
      return emailCheckedRegex.test(this.email);
    },
    isEmailError() {
      return !this.isEmailValid && this.isEmailTouched && !this.isInputUserEmailEmpty;
    },
    isInputUserEmailEmpty() {
      return !this.email && this.isEmailTouched;
    },
    isInputFirstNameEmpty() {
      return !this.first_name && this.isFirstNameTouched;
    },
    isInputLastNameEmpty() {
      return !this.last_name && this.isLastNameTouched;
    },
  }
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
  #selectProductType > div {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
  }
  #checkboxForm {
    width: 100%;
  }


  .closeTab {
    cursor: pointer;
    font-size: 2rem;
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
  .def {
    outline: 0;
    box-shadow: none;
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
    resize: none;
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
  .error {
    color: red;
    border: 1px solid red;
    background-color: rgba(255, 85, 85, 0.281);
  }
  .error:focus {
    border: 1px solid red;
    outline:1px solid  red;
  }
</style>
