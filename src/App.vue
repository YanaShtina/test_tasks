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
      let  date1 = calendar.date[0];
      let  date2 = calendar.date[1];


        // написать фунцию, чтобы перебрать массив, 
        let event = new Date(date1);
        let dateNew = JSON.stringify(event)
        date1 = dateNew.slice(1,11);

        let event2 = new Date(date2);
        let dateNew2 = JSON.stringify(event2)
        date2 = dateNew2.slice(1,11);

      this.result = `url/?params={adult: ${adult},childQ:${chilQ},childAge:${child},dateFrom: ${date1} ,dateto: ${date2}}`; 
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
