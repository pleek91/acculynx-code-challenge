<template>
  <div class="phone-number row flex-align-center input-group">
    <div class="col flex-grow-none">
      <button type="button" class="button button--red" title="Remove phone number" @click="$emit('remove', index)">X</button>
    </div>
    <div class="col-3">
      <select name="phone_type" id="phone_type" class="input" v-model="type">
        <option value="work">Work</option>
        <option value="cell">Cell</option>
        <option value="home">Home</option>
      </select>
    </div>
    <div class="col">
      <input type="tel" class="input" :name="affix('phone')" :id="affix('phone')" placeholder="(815) 979 9927 +101" v-model="value">
    </div>
    <div class="col flex-grow-none">
      <label class="input-radio" title="Make primary phone number">
        <input type="radio" name="phone-primary" :id="affix('phone-primary')" :value="index" :checked="isPrimary">
        <span class="radio__checkmark"></span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PhoneNumber',
  props: {
    name: {
      default: 'phone',
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
      , type: 'work'
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
