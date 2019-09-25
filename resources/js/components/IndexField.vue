<template>
  <div class="flex flex-col items-center">
    <img v-if="src" :src="src" style="object-fit: cover;" class="rounded-full w-8 h-8" />

    <span v-else class="text-xs">No thumbnail</span>
  </div>
</template>

<script type="text/babel">
export default {
  props: ['resourceName', 'field'],

  data() {
    return {
      src: ''
    };
  },

  mounted() {
    this.onGetThumbnail();
  },

  methods: {
    onGetThumbnail() {
      const xhr = new XMLHttpRequest();
      const url = `http://vimeo.com/api/v2/video/${this.field.value}.xml`;
      xhr.open('GET', url);
      xhr.send();

      xhr.onload = () => {
        if (xhr.status === 200) {
          const parser = new DOMParser();
          const xmlDoc = parser.parseFromString(xhr.responseText, 'text/xml');

          this.src = xmlDoc.getElementsByTagName('thumbnail_small')[0].innerHTML;
        }
      };
    }
  }
};
</script>
