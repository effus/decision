<template>
    <div class="rating">
        <a href="javascript:" :class="{'text-yellow-500': hover.s1, 'bg-dark': value === 1}" 
            v-on:click="onClick('s1')">
            <i class="fa fa-star"></i></a>
        <a href="javascript:" :class="{'text-yellow-500': hover.s2, 'bg-dark': value === 2}" 
            v-on:click="onClick('s2')">
            <i class="fa fa-star"></i></a>
        <a href="javascript:" :class="{'text-yellow-500': hover.s3, 'bg-dark': value === 3}" 
            v-on:click="onClick('s3')">
            <i class="fa fa-star"></i></a>
        <a href="javascript:" :class="{'text-yellow-500': hover.s4, 'bg-dark': value === 4}" 
            v-on:click="onClick('s4')">
            <i class="fa fa-star"></i></a>
        <a href="javascript:" :class="{'text-yellow-500': hover.s5, 'bg-dark': value === 5}" 
            v-on:click="onClick('s5')">
            <i class="fa fa-star"></i></a>
    </div>
</template>

<script>
export default {
    name: 'rating',
    props: {
        value: {
            type: Number|Object
        },
        meta: {
            type: Object
        }
    },
    data() {
        return {
            list: ['s1', 's2', 's3', 's4', 's5'],
            hover: {
                s1: false,
                s2: false,
                s3: false,
                s4: false,
                s5: false
            }
        }
    },
    methods: {
        onMouseOver(s) {
            
        },
        onClick(s) {
            for (let i in this.list) {
                this.hover[this.list[i]] = false;
            }
            for (let i in this.list) {
                this.hover[this.list[i]] = true;
                if (this.list[i] === s) {
                    this.$emit('click', {
                        value: parseInt(i)+1,
                        meta: this.meta
                    });
                    break;
                }
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.rating {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
    a {
        padding: 0;
        justify-items: center;
        justify-self: center;
    }
}
</style>