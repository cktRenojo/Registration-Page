<template>
  <q-layout>
  
    <q-page-container>
 
      <q-page class="q-pa-md">
        <Registration />
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import Registration from '~/components/Registration.vue'

export default {
  components: {
    Registration
  }
}

</script>

<style>
html,
body {
  height: 1297px;
  margin: 0;
  background: linear-gradient(
    0deg,
    rgba(151, 42, 177, 1) 0%,
    rgba(28, 58, 112, 1) 80%,
    rgba(8, 24, 50, 1) 100%
  );
}
</style>
