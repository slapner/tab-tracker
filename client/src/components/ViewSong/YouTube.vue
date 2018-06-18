<template>
<panel title="YouTube Video" class="text-xs-center">
  <youtube
    :video-id="youtubeId">
  </youtube>
</panel>
</template>

<script>
export default {
  props: [
    'youtubeId'
  ]
}
</script>

<style>

</style>
