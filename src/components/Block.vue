<template>
    <div class="block-container">
        <div class="block" v-if="showBlock" @click="stopTimer">
        <p>CLICK ME!</p>
        </div>
        <div class="pre-block" v-else @click="tooEarly">
            <p>watch out here</p>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'delay'
    ],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0,
            showDeadSpace: true
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true;
            this.startTimer();
        }, this.delay);
    },
    // updated() {
    //     console.log('component updated');
    // },
    // unmounted() {
    //     console.log('component unmounted');
    // }
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            }, 10);
        },
        stopTimer() {
            clearInterval(this.timer);
            console.log(this.reactionTime);
            this.$emit('end', this.reactionTime);
        },
        tooEarly() {
            this.$emit('tooEarly');
        }
    },
    emits: [
        'end',
        'tooEarly'
    ]
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=PT+Mono&display=swap');

    .block-container {
        padding: 0 15px;
    }

    .block,
    .pre-block {
        font-family: 'PT Mono', monospace;
        background-color: #11999E;
        max-width: 400px;
        border-radius: 20px;
        font-size: 1.4rem;
        text-align: center;
        padding: 80px 0;
        margin: 45px auto;
        cursor: pointer;
    }

    .pre-block {
        opacity: 0.6;
    }
</style>