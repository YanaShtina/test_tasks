<template>
  <div class="select">
    <div  class="select__top top">Туристы</div>
    <div> {{adult}} взрослых</div>
    <div 
    v-if="isSelectOpened"
    class="select__body">

      <div 
      class="select__adult"
      > 
        <span 
        @click="incr"
        >
        -
        </span>   
        {{adult}} взрослых    
        <span
        @click="decr"
      
        >+</span> 
      </div>

      <div  class="select__children"
      @click= "toggleChildrenOpened">
        Добавить ребенка

        <ul class="select__children-list">
          <div class="select__children-item"
          v-for="child, i in children"
          :key=i>
          выбран ребенок {{ child }}
        </div>
        </ul>

        <ul class="children"
        v-if="isChildrenOpened">
          <li
          v-for="option, i in opt"
          @click="pushChild(option)"
          :key=i
          > {{ option }}</li>
        </ul>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      adult: 2,
      opt: ['Меньше 2 лет', '2','3','4','5','6','7','8','9','10','11'],
      children: [],
      isSelectOpened: true,
      isChildrenOpened: false,
    }
  },

  methods: {
    decr() {
      this.adult += 1;
    },
    incr() {
      this.adult -= 1;
    },
    toggleChildrenOpened() {
      this.isChildrenOpened = !this.isChildrenOpened
    },
    pushChild(option) {
      this.children.push(option);
      console.log('pushChild', option);
    }
  }

}
</script>

<style lang="scss">
$b: '.select';

#{$b} {
  $a-blue: #2b51e7;
  max-width: 250px;
  &__top {
    margin-bottom: 15px;
  }

  &__body {
    padding: 10px;
    border: 1px solid lightcoral;
  }

  &__adult {
    margin-bottom: 10px;
  }
  
  ul {
    padding: 0;
  }

  li {
    list-style: none;
    padding: 0;
  }
  &__children-item {
    color: #2b51e7;
  }
}

</style>