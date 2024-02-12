<template>
    <div>
    <h2>{{ firstName }}</h2>
    <h3>{{ LAST }}</h3>
    <h4>{{ fullName }}</h4>
    <button @click="$emit('emit-something')">Emit something</button>
<user-temp></user-temp>
</div>
</template>


<script setup>
import { computed,defineProps,ref, defineEmits,onUnmounted,onBeforeUnmount } from 'vue';
import UserTemp from './UserTemp.vue';

    const props=defineProps(['firstName','LAST']);
    defineEmits(['emit-something']);   // vue 3 emitts

    console.log(props);
    const firstName= ref(props.firstName);
    const LAST= ref(props.LAST);
    //props:['firstName', 'LAST'],

     const fullName= computed(function (){
            return props.firstName + " "+ props.LAST;
        } );

onBeforeUnmount(function(){
    console.log('On before unmounted');
    alert('component is going to be umounted');
});

onUnmounted(function(){
    console.log('on unmounted');
});


</script>