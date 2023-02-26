<template>
  <div class="container">
    <app-calendar>  </app-calendar>
    <app-Turists>  </app-Turists>

    <button
    > найти туры</button>
  </div>


</template>

<script>

import AppCalendar from '@/components/AppCalendar.vue'
import AppTurists from '@/components/AppTurists.vue'
export default {
  name: 'App',
  components: {
    AppCalendar,
    AppTurists
  },

}
</script>

<style lang="scss">
$a-blue: #2b51e7;

.container {
  display: flex;
  align-items: center;
}

</style>
