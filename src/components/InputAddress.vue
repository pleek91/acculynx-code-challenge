<template>
  <div class="address">
    <div class="input-group">
      <label :for="affix('street_address')" class="label">Street Address</label>
      <input type="text" class="input" :name="affix('street_address')" id="street_address" placeholder="123 State St.">
    </div>
    <div class="input-group">
      <label :for="affix('street_address_2')" class="label">Street Address Line 2</label>
      <input type="text" class="input" :name="affix('street_address_2')" id="street_address_2" placeholder="Suite #5">
    </div>
    <div class="row">
      <div class="col">
        <div class="input-group">
          <label :for="affix('city')" class="label">City</label>
          <input type="text" :id="affix('city')" class="input" placeholder="New York City">
        </div>
      </div>
      <div class="col">
        <div class="input-group">
          <label :for="affix('state')" class="label">State</label>
          <select :id="affix('state')" class="input">
            <option value="">-- Select a State --</option>
            <option value="AL">Alabama</option>
            <option value="AK">Alaska</option>
            <option value="AZ">Arizona</option>
            <option value="AR">Arkansas</option>
            <option value="CA">California</option>
            <option value="CO">Colorado</option>
            <option value="CT">Connecticut</option>
            <option value="DE">Delaware</option>
            <option value="DC">District Of Columbia</option>
            <option value="FL">Florida</option>
            <option value="GA">Georgia</option>
            <option value="HI">Hawaii</option>
            <option value="ID">Idaho</option>
            <option value="IL">Illinois</option>
            <option value="IN">Indiana</option>
            <option value="IA">Iowa</option>
            <option value="KS">Kansas</option>
            <option value="KY">Kentucky</option>
            <option value="LA">Louisiana</option>
            <option value="ME">Maine</option>
            <option value="MD">Maryland</option>
            <option value="MA">Massachusetts</option>
            <option value="MI">Michigan</option>
            <option value="MN">Minnesota</option>
            <option value="MS">Mississippi</option>
            <option value="MO">Missouri</option>
            <option value="MT">Montana</option>
            <option value="NE">Nebraska</option>
            <option value="NV">Nevada</option>
            <option value="NH">New Hampshire</option>
            <option value="NJ">New Jersey</option>
            <option value="NM">New Mexico</option>
            <option value="NY">New York</option>
            <option value="NC">North Carolina</option>
            <option value="ND">North Dakota</option>
            <option value="OH">Ohio</option>
            <option value="OK">Oklahoma</option>
            <option value="OR">Oregon</option>
            <option value="PA">Pennsylvania</option>
            <option value="RI">Rhode Island</option>
            <option value="SC">South Carolina</option>
            <option value="SD">South Dakota</option>
            <option value="TN">Tennessee</option>
            <option value="TX">Texas</option>
            <option value="UT">Utah</option>
            <option value="VT">Vermont</option>
            <option value="VA">Virginia</option>
            <option value="WA">Washington</option>
            <option value="WV">West Virginia</option>
            <option value="WI">Wisconsin</option>
            <option value="WY">Wyoming</option>
          </select>
        </div>
      </div>
      <div class="col">
        <div class="input-group">
          <label :for="affix('zip_code')" class="label">Zip Code</label>
          <input type="text" :id="affix('zip_code')" class="input" placeholder="10004">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Address',
  props: ['prefix'],
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
