<template>
    <div :style="selfStyle" @click="onCellClick(cellNum)" class="cell-num-wrapper">
        <span class="num-p">{{ cellText }} </span>
    </div>
</template>

<script>
export default {
    name: 'cell',
    data() {
        return {
            selfStyle: {
                'color': 'black',
                'background-color': '#ffe0b2'
            },
            clicked: false
        }
    },
    props: {
        cellNum: {
            required: true
        },
        cellText: {
            required: true
        },
        resetFlag: {
            required: true
        }
    },
    watch: {
        resetFlag: {
            // eslint-disable-next-line
            handler: function(val, oldVal) {
                // reset style
                this.selfStyle['color'] = 'black'
                this.selfStyle['background-color'] = '#ffe0b2'
                // enable click
                this.clicked = false
            }
        }
    },
    methods: {
        onCellClick(cellNum) {
            if (this.clicked) {
                this.clicked = false
                this.selfStyle['color'] = 'black'
                this.selfStyle['background-color'] = '#ffe0b2'
            }else{
                this.clicked = true
                this.selfStyle['color'] = 'white'
                this.selfStyle['background-color'] = '#00897b'
                this.$emit('correct', cellNum)
            } 
        }
    },
    mounted() {
        // reset style
        this.selfStyle['color'] = 'black'
        this.selfStyle['background-color'] = '#ffe0b2'
    }
}
</script>

<style>
.cell-num-wrapper {
    height: 100%;
    width: 100%;
}
.cell-num-wrapper>span {
    display: inline-block;
    padding-top: 25%;
    font-size: small;
    line-height: 1.3em;
}
</style>
