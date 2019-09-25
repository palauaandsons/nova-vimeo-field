<template>
  <panel-item :field="field">
    <template v-if="field.value" slot="value">
      <iframe
        :src="'https://player.vimeo.com/video/' + field.value + '?title=0&byline=0&portrait=0'"
        allow="autoplay; fullscreen"
        allowfullscreen
        frameborder="0"
        height="400"
        width="640"
      ></iframe>
    </template>
  </panel-item>
</template>

<script type="text/babel">
export default {
  props: ['resource', 'resourceName', 'resourceId', 'field']
};
</script>
