<template>
    <div class="message-body">
        <p>That's it for the first stage of the experiment! Click the button to take a test about what you just did. When you're done click on Continue to go to the second stage.</p>
        <a class="button" href="https://cornell.qualtrics.com/jfe/form/SV_aeJIreVxXrtrUAR" target="_blank" v-on:click="changeButtons" v-if="firstButton">Take test</a>
        <a class="button" v-on:click.prevent="goToNextStage" v-if="!firstButton">Continue</a>
    </div>
</template>

<script>
    export default {
        name: 'stage1-modal',
        data() {
            return {
                firstButton: true
            }
        },
        methods: {
            goToNextStage() {
                let currentStage = this.$store.state.experiment.experimentStage;
                let nextStage = this.$store.state.experiment.stageInformation[currentStage].nextStage;
                console.log(currentStage, nextStage);
                this.$store.dispatch('startStage', nextStage).then(() => {
                    this.$store.commit('setExperimentStage', nextStage);
                    this.$emit('close-modal');
                });
            },
            changeButtons() {
                this.firstButton = false;
            }
        }
    }
</script>

<style scoped>

</style>