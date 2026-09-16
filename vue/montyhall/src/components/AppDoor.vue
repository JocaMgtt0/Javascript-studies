<template>
    
    <div class="door-area">
        <div class="door-frame">
            <AppGif />
        </div>
        <div class="door">
            <div class="number">{{ number }}</div>
            <div class="knob"></div>
        </div>
    </div>

</template>

<script>
import AppGif from './AppGif.vue';


export default {
    name: 'AppDor',
    components: {AppGif},
    props:{
        number: {},
        hasGift: {type: Boolean}
    },
    data: function (){
        return {
            open: false,
            selected: false
        }
    }
}
</script>


<style>

</style>