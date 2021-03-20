<template>
  <div class="paragraph">
    <h3>{{ content.metdata.pres_title }}</h3>
    <div class="begin">{{ content.metdata.pres_first }}</div>
    <p>{{ content.metdata.pres_second }}</p>
  </div>
</template>

<script>
export default {
  name: "Description",
  props: ["content"],
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

.paragraph {
  color: map-get($colors, primary);
  .begin {
    color: map-get($colors, secondary);
  }
}
</style>