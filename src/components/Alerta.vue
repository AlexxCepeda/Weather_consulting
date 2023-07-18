<template>
  <div class="alert">
    <slot></slot>
  </div>
</template>

<style scoped>
.alert {
  padding: 1rem;
  width: 100%;
  background-color: rgb(230, 66, 66);
  text-align: center;
  margin-bottom: 2rem;
  color: #fff;
  font-size: 1.6rem;
  line-height: 1.8rem;
  text-transform: uppercase;
  font-weight: 700;
}
</style>
