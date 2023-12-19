<script setup>
const isDrillDown = ref(false)
const oppositeIsDrillDown = () => {
  isDrillDown.value = !isDrillDown.value
}
</script>
<template>
  <Html lang="en">
    <Head>
      <Title>title</Title>
      <Meta
        name="description"
        content="`My page's description`"
      />
    </Head>
  </Html>
  <div>
    <Country
      v-show="!isDrillDown"
      @handle-click="oppositeIsDrillDown"
    />
    <Province
      v-show="isDrillDown"
      @handle-click="oppositeIsDrillDown"
    />
  </div>
</template>
<style scoped></style>
