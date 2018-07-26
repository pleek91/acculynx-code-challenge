<template>
  <div id="app">
    <form method="POST">
      <header class="page-header">
        <div class="container">
          <h1>AccuLynx</h1>
        </div>
      </header>
      <div class="container">
        <h2>Create A New Contact</h2>
        <p>Complete the form below and press "Save Contact" to create a new contact.</p>
        <div class="section">
          <h3>Basic Information</h3>
          <div class="row">
            <div class="col">
              <label for="salutation" class="label">Name <span class="label__required">*</span></label>
              <div class="input-group row">
                <div class="col-2">
                  <input type="text" class="input" name="salutation" id="salutation" placeholder="Mr.">
                </div>
                <div class="col">
                  <input type="text" class="input" name="first_name" id="first_name" placeholder="John">
                </div>
                <div class="col">
                  <input type="text" class="input" name="last_name" id="last_name" placeholder="Smith">
                </div>
              </div>
              <div class="input-group">
                <label for="company_name" class="label">Company Name <span class="label__required">*</span></label>
                <input type="text" class="input input--invalid" name="company_name" id="company_name">
                <p class="input-msg input-msg--invalid">Company name is required</p>
              </div>
            </div>
            <div class="col-lg flex-grow-none">
              <div class="input-group">
                <InputPhoto name="photo" id="photo"></InputPhoto>
              </div>
            </div>
          </div>
        </div>
        <div class="section">
          <h3>Contact Information</h3>
          <div class="row row--gutters-lg">
            <div class="col-lg">
              <div class="input-group">
                <label for="phone-1" class="label">Phone Number(s)</label>
                <p class="input-msg">Add one or more phone numbers for this contact.</p>
              </div>
              <InputPhoneNumber v-for="(phone, index) in phones" :key="phone.id" v-bind:allowRemove="true" v-bind:allowPrimary="true" v-bind:suffix="index" v-bind:index="index" v-on:remove="removePhoneNumber(index)"></InputPhoneNumber>
              <div class="input-group">
                <button type="button" class="button button--small button--gray" @click="addPhoneNumber()">Add Another</button>
              </div>
            </div>
            <div class="col-lg">
              <div class="input-group">
                <label for="email-1" class="label">Email Address(es)</label>
                <p class="input-msg">Add one or more email addresses for this contact.</p>
              </div>
              <InputEmailAddress v-for="(email, index) in emails" :key="email.id" v-bind:allowRemove="true" v-bind:allowPrimary="true" v-bind:suffix="index" v-bind:index="index" v-on:remove="removeEmailAddress(index)"></InputEmailAddress>
              <div class="input-group">
                <button type="button" class="button button--small button--gray" @click="addEmailAddress()">Add Another</button>
              </div>
            </div>
          </div>
        </div>
        <div class="section">
          <h3>Mailing Address</h3>
          <InputAddress prefix="mailing"></InputAddress>
        </div>
        <div class="section">
          <h3>Billing Address</h3>
          <label class="input-group input-checkbox">
            Same As Mailling Address
            <input type="checkbox" name="billing-same-as-mailing" v-model="billingSameAsMailing">
            <span class="checkbox__checkmark"></span>
          </label>
          <InputAddress v-if="!billingSameAsMailing" prefix="billing"></InputAddress>
        </div>
      </div>
      <footer class="page-footer">
        <div class="container text-right">
          <button class="button button--large button--teal" type="submit">Save Contact</button>
        </div>
      </footer>
    </form>
  </div>
</template>

<script>
import InputAddress from './components/InputAddress.vue'
import InputEmailAddress from './components/InputEmailAddress.vue'
import InputPhoneNumber from './components/InputPhoneNumber.vue'
import InputPhoto from './components/InputPhoto.vue'

export default {
  name: 'app',
  components: {
    InputAddress,
    InputEmailAddress,
    InputPhoneNumber,
    InputPhoto
  },
  data: function() {
    return {
      billingSameAsMailing: true,
      emails: [{ id: 1 }],
      phones: [{ id: 1 }]
    }
  },
  methods: {
    addEmailAddress: function() {
      // fake ids. Add 1 to the last used id or use 1 if no ids
      this.emails.push({ id: this.emails.length ? this.emails[this.emails.length - 1].id + 1 : 1 });
    },
    removeEmailAddress: function(index) {
      this.emails.splice(index, 1);
    },
    addPhoneNumber: function() {
      // fake ids. Add 1 to the last used id or use 1 if no ids
      this.phones.push({ id: this.phones.length ? this.phones[this.phones.length - 1].id + 1 : 1 });
    },
    removePhoneNumber: function(index) {
      this.phones.splice(index, 1);
    },
  }
}
</script>

<style lang="scss">

// 
// Variables & Settings
// 

// Theme colors
$theme: (
  teal: #007EA7,
  gray: #C5C3C6,
  red: #A63446
);

// Reusable property values
$transition: all 0.15s ease-in-out;
$border-radius: 5px;


// 
// Global Element & Pseudo-Element Styles
// 

*, ::after, ::before {
  box-sizing: border-box;
  line-height: 1.5;
}

body, html {
  padding: 0;
  margin: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  color: #1b1b1b;
}

h1, h2, h3, p {
  margin: 0 0 1rem;
}

h1 {
  font-size: 2rem;
}

h2 {
  font-size: 1.5rem;
}

h3 {
  font-size: 1.25rem;
}

p {
  font-size: 1rem;
}

::placeholder {
  color: #999;
}


// 
// Page Header
// 

header.page-header,
footer.page-footer {
  border-bottom: 2px solid darken(#e7f0f3, 10%);
  box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.25);
  background-color: #e7f0f3;
  position: sticky;
  padding: 10px 0;
  z-index: 100;
}

header.page-header {
  margin-bottom: 50px;
  top: 0;
  
  h1 {
    margin: 0;
  }
}

footer.page-footer {
  margin-top: 50px;
  bottom: 0;
}


// 
// Layout Classes
// 

.container {
  width: 979px;
  max-width: 90%;
  margin: 0 auto;
}

.section {
  margin: 30px 0;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-left: -5px;
  margin-right: -5px;
  
  > [class^=col] {
    margin-left: 5px;
    margin-right: 5px;
    max-width: 100%;
  }
  
}

.row--gutters-lg {
  margin-left: -20px;
  margin-right: -20px;
  
  > [class^=col] {
    margin-left: 20px;
    margin-right: 20px;  
  }
  
}

.col {
  flex-basis: 0;
  flex-grow: 1;
}

// Fixed percentage widths for numbered columns (1-12)
@for $i from 1 through 12 {
  .col-#{$i} {
    flex: 0 0 percentage($i / 12);
    max-width: percentage($i / 12);
  }
}

.col-lg {
  width: 100%;
  @media (min-width: 720px) {
    flex-basis: 0;
    flex-grow: 1;
  }
}

// Fixed percentage widths for numbered columns (1-12)
@for $i from 1 through 12 {
  @media (min-width: 720px) {
    .col-lg-#{$i} {
      flex: 0 0 percentage($i / 12);
      max-width: percentage($i / 12);
    }
  }
}


// 
// Buttons
// 

.button {
  border-radius: $border-radius;
  transition: $transition;
  vertical-align: middle;
  text-decoration: none;
  display: inline-block;
  padding: 6px 12px;
  font-weight: 400;
  cursor: pointer;
  font-size: 1em;
  color: #fff;
  border: 0;
  
  &:disabled {
    opacity: 0.65;
    cursor: not-allowed;
  }
  
}

.button--wide {
  text-align: center;
  display: block;
}

.button--large {
  padding: 0.5em 0.75em;
  font-size: 18px;
}

.button--small {
  padding: 0.25em 0.5em;
  font-size: 14px;
}

// Styles for individual theme'd button
@each $name, $color in $theme {
  
  .button--#{$name} {
    background-color: $color;
    box-shadow: 0px 0px 0px 1px $color;
    
    &:active {
      box-shadow: inset 0px 2px 20px 0px darken($color, 20%),
                  0px 0px 0px 2px #fff,
                  0px 0px 0px 4px lighten($color, 10%);
    }
    
    &:focus {
      box-shadow: 0px 0px 0px 2px #fff,
                  0px 0px 0px 4px lighten($color, 10%);
      outline: 0;
    }
    
    // :not(:disabled) because a disabled button should not have a hover style
    &:not(:disabled):hover {
      background-color: darken($color, 10%);
    }
    
  }
  
}


// 
// Form Elements
// 

.input-group {
  margin-bottom: 0.75rem;
}

.input {
  box-shadow: 0px 0px 0px 1px map-get($theme, gray);
  border-radius: $border-radius;
  padding: 0.375rem 0.75rem;
  transition: $transition;
  font-size: 1rem;
  display: block;
  width: 100%;
  border: 0;
  
  &:disabled {
    opacity: 0.65;
    cursor: not-allowed;
  }
  
  &:focus {
    box-shadow: 0px 0px 0px 1px #fff,
                0px 0px 0px 3px map-get($theme, gray);
    border-color: transparent;
    outline: 0;
  }
  
}

// fixes height missmatch. line-height + padding-top + padding-bottom
select.input {
  height: calc(1.5rem + 0.375rem + 0.375rem); 
}

.input--invalid {
  box-shadow: 0px 0px 0px 1px map-get($theme, red);
  color: map-get($theme, red);
  
  &:focus {
    box-shadow: 0px 0px 0px 1px #fff,
                0px 0px 0px 3px map-get($theme, red);
    border-color: transparent;
    outline: 0;
  }
  
}

.label {
  display: inline-block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  
  + .input-msg {
    margin-top: -0.5rem;
  }
  
}

.label__required {
  color: map-get($theme, red);
}

.input-msg {
  font-size: 14px;
  font-weight: 600;
}

.input-msg--invalid {
  color: map-get($theme, red);
}

.input-checkbox, .input-radio {
  display: inline-block;
  padding-left: 25px;
  position: relative;
  user-select: none;
  min-height: 24px;
  cursor: pointer;
  
  input[type="checkbox"], input[type="radio"] {
    position: absolute;
    opacity: 0;
    height: 0;
    width: 0;
    
    &:checked + .checkbox__checkmark:before,
    &:checked + .radio__checkmark:before, {
      width: 12px;
      height: 12px;
    }
  }
  
}

.checkbox__checkmark, .radio__checkmark {
  border: 2px solid map-get($theme, gray);
  transform: translateY(-50%);
  position: absolute;
  height: 20px;
  width: 20px;
  top: 50%;
  left: 0;
  
  &:before {
    background-color: map-get($theme, gray);
    transform: translate(-50%, -50%);
    transition: $transition;
    position: absolute;
    display: block;
    content: '';
    height: 0%;
    width: 0%;
    left: 50%;
    top: 50%;
  }
}

.radio__checkmark {
  border-radius: 50%;
  
  &:before {
    border-radius: 50%;
  }
  
}


// 
// Photo Input
// 

.input-photo {
  max-width: 100%;
  width: 200px;
}

.input-photo__preview {
  border: 2px solid map-get($theme, gray);
  background-position: center center;
  background-size: cover;
  margin-bottom: 0.5em;
  position: relative;
  cursor: pointer;
  display: block;
  height: 200px;
}

.input-photo__preview--empty:before {
  color: map-get($theme, gray);
  transform: translateY(-50%);
  content: 'Choose A Photo';
  text-align: center;
  position: absolute;
  font-weight: 600;
  display: block;
  width: 100%;
  top: 50%;
}


// 
// Utility Classes (last so they override any previous class's styles)
// 

.text-right {
  text-align: right;
}

.flex-right {
  margin-left: auto;
}

.flex-grow-none {
  flex-grow: 0;
}

.flex-align-center {
  align-items: center;
}
</style>
