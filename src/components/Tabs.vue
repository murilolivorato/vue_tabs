<template>
  <div class="tabs_data">
    <ul v-bind:id="nametab" v-bind:class="classname" >
      <li v-for="(tab, index) in tabTitles" :class="verifyActive(tab)"
          :key="index">
        <a href="#"  @click.prevent="selectedTitle = tab.value"> {{ tab.title }}</a>
      </li>
    </ul>
    <slot/>
  </div>
</template>

<script>
import { ref, provide, watchEffect } from 'vue'
export default {
  props: {
    nametab: { type: String },
    classname: { type: String, default: null }
  },
  setup (props, { slots, emit }) {
    const formIsSetted = ref(false)
    const tabTitles = ref(slots.default().flatMap((tab) => tab.props !== null ? tab.props : []))
    const isSelected = ref(Object.fromEntries(Object.entries(tabTitles.value).filter(([key, value]) => value.active === true )))
    const selectedId = Object.keys(isSelected.value).length ? Object.keys(isSelected.value)[0] : null
    //const selectedTitle = ref(tabTitles.value[0].value)
    const selectedTitle = ref(tabTitles.value[selectedId].value)
    provide('selectedTitle', selectedTitle)
    watchEffect(() => {
      if(selectedTitle.value && formIsSetted.value) {
        emit('changestatustab', selectedTitle.value)
      }
      formIsSetted.value = true

    })
    return {
      selectedTitle,
      tabTitles,
      formIsSetted,
      isSelected
    }
  },
  methods: {
    verifyActive (tab) {
      if (tab.value === this.selectedTitle) {
        return 'is-active'
      }
    }
  }
}
</script>

<style scoped>
ul.menu_type_slider_one {
  margin:0px auto;
  padding:10px 0 20px 0;
  display: flex;
  justify-content: center;

}
ul.menu_type_slider_one.is_left {
  justify-content: left;
}
ul.menu_type_slider_one.is_center {
  justify-content: center;
}
ul.menu_type_slider_one li {
  display: inline-block;
  padding:0 16px 0 0 !important;
}
ul.menu_type_slider_one li a {
  border-radius:50px;

  padding:12px 20px 12px 20px;
  display:block;
  font-size: 17px;
  font-family:Myfont, Helvetica, Arial, Sans-Serif;
  color: #202426;
  -webkit-box-shadow: 2px 2px 2px 0 rgba(173,173,173,0.70) ;
  box-shadow: 2px 2px 2px 0 rgba(173,173,173,0.70) ;
  border-bottom:#eeeeee 1px solid;
  background:#FFF;
}
ul.menu_type_slider_one li.is-active a {
  background: #0e9129;
  color: #FFF;
  border-bottom:#818DA2FF 1px solid;
  -webkit-box-shadow: 2px 2px 2px 0 rgba(62,128,165,0.50) ;
  box-shadow: 2px 2px 2px 0 rgba(62,128,165,0.3) ;
}

ul.menu_type_slider_one li a:hover {
  border-bottom: #818DA2FF 1px solid;
  -webkit-box-shadow: 2px 2px 2px 0 rgba(62,128,165,0.50) ;
  box-shadow: 2px 2px 2px 0 rgba(62,128,165,0.3) ;
}

ul.tabs li {
  padding-bottom:25px !important;
}
</style>
