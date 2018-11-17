<template>
    <Page>
        <Button text="nav" @tap="nav"></Button>
    </Page>
</template>

<script>
import Vue from 'vue';
import App from './App';

export default Vue.extend({
    methods: {
        nav() {
            this.$navigateTo(App);
        }
    }
});
</script>

<style>

</style>
