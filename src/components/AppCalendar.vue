<template>
    <div class="calendar">
    <div  class="calendar__top top">Даты</div>
    <date-picker
      v-model="date"
      type="format"
      format='dd/MM/yyyy'
      range
      auto-apply
      :min-date="new Date()" 
      :enable-time-picker="false"
      placeholder=" Выбрать даты"
    >
    </date-picker>
  </div>
</template>

<script>
import DatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

export default {
  name: 'AppCalendar',
  components: {
    DatePicker,
  },
  data() {
    return {
      date: '',
      sendData:'',
    }
  },
  methods: {
    alertDate() {

    }
  }
}
</script>

<style lang="scss">
$b: '.calendar';

#{$b} {
  $a-blue: #2b51e7;
  width: 250px;
  margin-right: 25px;
  &__top {
    margin-bottom: 15px;
  }

  .dp__input {
    font-size: 14px;
  }

  .dp__input:hover, 
  .dp__input:focus {
    border-color: $a-blue;
  }

  .dp__calendar_header_item {
    font-weight: 400;
  }

  .dp__cell_disabled {
    cursor: initial;
  }
}

</style>