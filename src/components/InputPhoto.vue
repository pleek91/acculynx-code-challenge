<template>
  <div class="input-photo">
    <label :for="this.id" class="label">Photo</label>
    <label :for="this.id" id="photo-preview" class="input-photo__preview" :class="{ 'input-photo__preview--empty': !hasPreview }" :style="{ 'background-image': 'url(' + preview + ')' }"></label>
    <label :for="this.id" class="button button--teal button--wide" tabindex="0">
      <input type="file" :name="this.name" :id="this.id" style="display: none;" accept="image/x-png,image/gif,image/jpeg" @change="updatePreview($event)">
      {{ action }}
    </label>
  </div>
</template>

<script>
export default {
  name: 'InputPhoto',
  props: {
    name: {
      default: 'photo',
      type: String
    },
    id: {
      default: 'photo',
      type: String
    }
  },
  data: function() {
    return {
      preview: '',
      color: 'blue'
    }
  },
  computed: {
    hasPreview: function() {
      return !!this.preview.length;
    },
    action: function() {
      return this.hasPreview ? 'Change' : 'Choose';
    }
  },
  methods: {
    updatePreview: function(event) {
      
      var vm     = this;
      var reader = new FileReader();

      reader.onload = function (e) {
        vm.preview = e.target.result;
      };

      reader.readAsDataURL(event.target.files[0]);
      
    }
  }
}
</script>
