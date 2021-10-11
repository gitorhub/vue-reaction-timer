<template>
    <div class="block" v-if="showBlock" @click="endTimer">
    </div>
</template>
<script>
    export default {
        props: ["delay"],
        data() {
            return {
                showBlock: false,
                timer: null,
                reactionTime: 0
            }
        },
        mounted() {
            setTimeout(() => {
                this.showBlock = true
                this.startTimer()
            }, this.delay);
        },
        methods: {
            startTimer() {
                this.timer = setInterval(() => {
                    this.reactionTime += 10
                }, 10);
            },
            endTimer() {
                clearInterval(this.timer)
                this.$emit("end", this.reactionTime)
                this.showBlock = false
            }
        },
    
    }
</script>
<style scoped>
    .block {
        width: clamp(320px,100vw,500px);
        padding: 150px 0;
        background: var(--success);
        margin: 50px auto;
        border-radius: var(--radius);
    }
</style>