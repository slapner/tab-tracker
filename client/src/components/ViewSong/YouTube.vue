<template>
<panel title="YouTube Video" class="text-xs-center">
  <youtube
    :video-id="youtubeId">
  </youtube>
</panel>
</template>

<script>
import Panel from '@/components/Panel'

export default {
  components: {
    Panel
  },
  props: [
    'youtubeId'
  ]
}
</script>

<style>

</style>
