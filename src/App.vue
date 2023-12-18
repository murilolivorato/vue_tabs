<template>
 <div class="container">
   <div class="columns has-text-centered">
     <div class="column">
       <h1>Cars</h1>
     </div>
   </div>
   <div class="columns">
     <div class="column">

         <tabs classname="menu_type_slider_one is_center"
               :showstatus="true"
               @changestatustab="changeStatusTab">
             <!-- SPECIAL FEATURE -->
             <tab title="Ford Mustang" value="ford_mustang" :active="true">
               <h2>Ford Mustang </h2>
               <figure class="image is-16by9">
                 <img src="/images/mustang.png" alt="Ford Mustang" />
               </figure>
               <p>The Ford Mustang, an emblem of American muscle and performance, first galloped onto the scene in 1964. Designed to appeal to the younger generation, the Mustang's sleek and sporty aesthetic captured the hearts of car enthusiasts worldwide. With its powerful V8 engine and unmistakable fastback design, the Mustang quickly became a symbol of freedom and the open road. Over the years, this classic pony car has undergone various transformations, adapting to modern tastes while retaining its timeless charm.</p>
             </tab>
             <tab title="Volkswagen Beetle" value="volkswagen_beetle" >
               <h2>Volkswagen Beetle </h2>
               <figure class="image is-16by9">
                 <img src="/images/volkswagen_beetle.png" alt="Ford Mustang" />
               </figure>
               <p>The Ford Mustang, an emblem of American muscle and performance, first galloped onto the scene in 1964. Designed to appeal to the younger generation, the Mustang's sleek and sporty aesthetic captured the hearts of car enthusiasts worldwide. With its powerful V8 engine and unmistakable fastback design, the Mustang quickly became a symbol of freedom and the open road. Over the years, this classic pony car has undergone various transformations, adapting to modern tastes while retaining its timeless charm.</p>
             </tab>
             <tab title="Ferrari 458 Italia" value="ferrari_458" >
               <h2>Ferrari 458 Italia</h2>
               <figure class="image is-16by9">
                 <img src="/images/ferrari_458_italia.png" alt="Ford Mustang" />
               </figure>
               <p>For enthusiasts with a penchant for Italian luxury and performance, the Ferrari 458 Italia stands as a testament to automotive excellence. Introduced in 2009, the 458 Italia quickly became a benchmark for supercars. Its mid-engine layout, breathtaking aerodynamics, and a high-revving V8 engine that produced an exhilarating symphony of power set it apart. The 458 Italia's precision handling and stunning design garnered acclaim from critics and enthusiasts alike, making it a modern classic in the Ferrari lineage.</p>
             </tab>
         </tabs>
     </div>
   </div>
 </div>
</template>
<script setup>
import Tabs from '@/components/Tabs.vue'
import Tab from '@/components/Tab.vue'

const changeStatusTab = async (status) => {
  console.log(status)
}
</script>
<style scoped>
h1 {
  font-size: 20px;
  text-transform: uppercase;
  padding-bottom: 30px;
}
h2 {
  padding-top:20px;
  padding-bottom: 20px;
  font-size: 21px;
  text-align:center;

}
p {
  padding-top:50px;
  font-size: 17px;
  line-height: 32px;
}
div.container {
  padding-top: 400px;
  width: 90%;
}
</style>
