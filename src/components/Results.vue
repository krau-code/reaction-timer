<template>
    <p class="displayScore">Reaction Time: <span>{{ displayScore / 1000 }} Seconds</span></p>
    <p class="rank" :class="{ white: color == 'white', 
                              green: color == 'green',
                              red: color == 'red' }">
        {{ rank }}
    </p>
</template>

<script>
export default {
    props: [
        'displayScore'
    ],
    data() {
        return {
            rank: null,
            color: null
        }
    },
    mounted() {
        if (this.displayScore < 250) {
            this.rank = 'REALLY FAST!';
            this.color = 'white';
        } else if (this.displayScore < 400) {
            this.rank = 'Fast Enough';
            this.color = 'green';
        } else {
            this.rank = 'Too Slow';
            this.color = 'red';
        }
    }
}
</script>

<style>
    .displayScore {
        margin-top: 40px;
        font-size: 0.9em;
    }
    
    .displayScore span {
        font-weight: bold;
    }

    .rank {
        display: inline-block;
        font-weight: bold;
        font-size: 1.6rem;
        padding: 15px;
        border-radius: 10px;
    }

    .rank.white {
        background: #E4F9F5;
        color: #40514E;
    }
    .rank.green {
        background: #0cc078;
    }
    .rank.red {
        background: #fb6962;
    }
</style>