<template>
<h3>{{ age.userAge }}</h3>
</template>

<script setup>

import { inject,ref } from 'vue';

const age= ref(inject('userage'));
</script>