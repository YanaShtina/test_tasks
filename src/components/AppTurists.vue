<template>
  <div class="select">
    <div  class="select__top top">Туристы</div>
    <div class="select__input input"
      @click="this.isSelectOpened = !this.isSelectOpened"
      :class="{ _active: isSelectOpened }"
      ref="selectBody1"> 
      <span v-if = "children.length === 0 ">{{adult}} взрослых</span>
      <span v-else> {{adult}} взр. + {{ children.length }} реб </span>
    </div>

    <div 
      v-if="isSelectOpened"
      class="select__body"
      ref="selectBody2"
      >

      <div class="select__adult"> 
        <span 
        @click="incr"
        class="select__adult-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M1.00012 8.00024C1.00012 7.44796 1.44784 7.00024 2.00012 7.00024L14.0001 7.00025C14.5524 7.00025 15.0001 7.44796 15.0001 8.00025C15.0001 8.55253 14.5524 9.00025 14.0001 9.00025L2.00012 9.00024C1.44784 9.00024 1.00012 8.55253 1.00012 8.00024Z" fill="#1B2640"/>
          </svg>
        </span>   
        <span class="select__adult-content"> {{adult}} взрослых </span>   
        <span @click="decr"
        class="select__adult-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M9.00004 2C9.00004 1.44772 8.55233 1 8.00004 1C7.44776 1 7.00004 1.44771 7.00004 2L7.00004 7.00016L2.00024 7.00016C1.44796 7.00016 1.00024 7.44788 1.00024 8.00016C1.00024 8.55245 1.44796 9.00016 2.00024 9.00016L7.00004 9.00016L7.00004 14C7.00004 14.5523 7.44775 15 8.00004 15C8.55232 15 9.00004 14.5523 9.00004 14L9.00004 9.00016L14.0002 9.00016C14.5525 9.00016 15.0002 8.55245 15.0002 8.00016C15.0002 7.44788 14.5525 7.00016 14.0002 7.00016L9.00004 7.00016L9.00004 2Z" fill="#1B2640"/>
          </svg>
        </span> 
      </div>

      <ul class="select__children-list">
          <div class="select__children-item"
          v-for="child, i in children"
          :key=i>
          выбран ребенок {{ ageTest(child) }}
        </div>
        </ul>

      <div  class="select__children input"
      @click= "toggleChildrenOpened"
      :class="{ _active: isChildrenOpened }">
        Добавить ребенка

      <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M12.7526 5.84151C13.1162 6.25715 13.0741 6.88891 12.6585 7.25259L8.65849 10.7526L7.99999 11.3288L7.34148 10.7526L3.34148 7.25259C2.92585 6.88891 2.88373 6.25715 3.24741 5.84151C3.61109 5.42587 4.24285 5.38375 4.65849 5.74744L7.99999 8.67125L11.3415 5.74744C11.7571 5.38375 12.3889 5.42587 12.7526 5.84151Z" fill="#1B2640"/>
      </svg>

        <ul class="select__age"
        v-if="isChildrenOpened">
          <li
          v-for="option, i in opt"
          @click.stop="pushChild(option)"
          :key=i
          > {{ ageTest(option) }}</li>
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
      opt: ['меньше 2','3','4','5','6','7','8','9','10','11'],
      children: [],
      isSelectOpened: false,
      isChildrenOpened: false,
    }
  },

  methods: {
    decr() {
      
      this.adult += 1;
    },
    incr() {
      if (this.adult <= 0) return;
      this.adult -= 1;
    },
    toggleChildrenOpened() {
      this.isChildrenOpened = !this.isChildrenOpened
    },
    pushChild(option) {
      this.children.push(option);
      this.isChildrenOpened = false;
    },
    ageTest(age) {
        let txt = '';
        let count = age % 10;
          if (!isNaN) {
            txt = `Меньше 2 лет`;
            return txt;
          } else if (count > 2 && count <= 4) {
            txt = 'года';
            return age + " " + txt;
          } else {
            txt = 'лет';
            return age + " " + txt;
          }
        
    },
    close(e) {
      let el1 = this.$refs.selectBody1;
      let el2 = this.$refs.selectBody2;
      let target = e.target;
      if (el1 == null || el2  == null) return;
      if (el1 !== target && el2 !== target  && !el1.contains(target) && !el2.contains(target)){
        this.isSelectOpened = false
      }
    }
  },
  created(){ 
    document.addEventListener('click', this.close)
  },
  mounted() {
    // console.log('ageTest: ', this.ageTest(4))
  },
  unmounted () {
    document.removeEventListener('click', this.close)
  }, 

}
</script>

<style lang="scss">
$b: '.select';

ul {
    padding: 0;
    margin: 0;
  }

  li {
    list-style: none;
  }

#{$b} {
  max-width: 250px;
  margin-right: 25px;
  position: relative;

  .input,
  &__input {
    padding: 0 6px;
    border: 1px solid #ddd;
    font-size: 14px;
    height: 38px;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

    &:hover {
      border-color: $a-blue;
      cursor: pointer;
    }

    &._active {
      border-color: $a-blue;
    }
  }

  &__top {
    margin-bottom: 15px;
  }

  &__body {
    padding: 10px;
    border: 1px solid $a-blue;
    border-radius: 4px;
    position: absolute;
    top: 110%;
    min-width: 200px;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #fff;
    z-index: 5;
  }

  &__adult {
    margin-bottom: 10px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;

    &-btn {
      width: 26px;
      height: 26px;
      border: 1px solid #ddd;
      border-radius: 100%;
      display: flex;
      align-items: center;
      justify-content: center;

      svg {
        width: 12px;
        height: 12px;
      }

      &:hover {
        border-color: $a-blue;
        cursor: pointer;
      }
    }

    &-content {
      margin: 0 15px;
      display: inline-block;
    }
  }

  &__children {
    width: 100%;
   
    &.input {
      padding: 0;
      position: relative;
    }

    svg {
      margin-left: 20px;
    }

    &._active {
      border-color: $a-blue;

      svg {
        transform: rotate(180deg);
      }
    }

    &-list {
      margin-bottom: 10px;
    }

    &-item {
      font-size: 16px;
      margin-bottom: 5px;
    }
  }

  &__age {
    padding: 15px;
    top: 105%;
    left: 0;
    width: 100%;
    background-color: #fff;
    z-index: 5;
    overflow-y: scroll;
    height: 200px;
    flex-direction: column;
    position: absolute;
    align-items: flex-start;
    justify-content: flex-start;
    border: 1px solid #ddd;
    border-radius: 4px;

    &::-webkit-scrollbar {
      width: 0;
      display: none;
    }

    li {
      font-size: 14px;
      padding: 5px;
    }
  }
}

</style>