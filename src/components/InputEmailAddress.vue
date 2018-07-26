<template>
  <div class="email-address row input-group flex-align-center">
    <div class="col flex-grow-none" v-if="allowRemove">
      <button type="button" class="button button--red" title="Remove email address" @click="$emit('remove', index)">X</button>
    </div>
    <div class="col">
      <input type="email" class="input" :name="affix('email')" :id="affix('email')" placeholder="johns@companyname.com" v-model="value">
    </div>
    <div class="col flex-grow-none" v-if="allowPrimary">
      <label class="input-radio" title="Make primary email address">
        <input type="radio" name="email-primary" :id="affix('email-primary')" :value="index" :checked="isPrimary">
        <span class="radio__checkmark"></span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EmailAddress',
  props: {
    name: {
      default: 'email',
      type: String
    },
    prefix: {
      default: '',
      type: [String, Number]
    },
    suffix: {
      default: '',
      type: [String, Number]
    },
    allowRemove: {
      default: false,
      type: Boolean
    },
    allowPrimary: {
      default: false,
      type: Boolean
    },
    isPrimary: {
      default: false,
      type: Boolean
    },
    index: Number
  },
  data: function() {
    return {
      value: ''
    }
  },
  methods: {
    affix: function(string) {
      if(this.prefix)
        string = this.prefix + '_' + string;
      
      if(this.suffix) 
        string = string + '_' + this.suffix;
      
      return string;
    }
  }
}
</script>
