<template>
  <div class="container">
    <app-calendar ref="calendar">  </app-calendar>
    <app-Turists ref="turists">  </app-Turists>

    <app-btn
    @click="sendData"> Найти тур</app-btn>
  </div>

  <div class="testString">{{ result }}</div>


</template>

<script>
import AppCalendar from '@/components/AppCalendar.vue'
import AppTurists from '@/components/AppTurists.vue'
import appBtn from '@/components/ui/appBtn.vue'
export default {
  name: 'App',
  components: {
    AppCalendar,
    AppTurists,
    appBtn
  },

  data() {
    return {
      result: '',
    }
  },

  methods: {
    sendData() {
      const tourists =  this.$refs.turists;
      const adult = tourists.adult;
      const chilQ = tourists.children.length;
      const [...child] = tourists.children; // возраст ребенка
      const calendar =  this.$refs.calendar;
      const  [...date] = calendar.date
      this.result = `url/?params={adult: ${adult},childQ:${chilQ},child:${child},date: ${date}}`; 
    }
  }

}
</script>

<style lang="scss">

.container {
  display: flex;
  align-items: center;
}

.testString {
  margin-top: 30px;
}

</style>
