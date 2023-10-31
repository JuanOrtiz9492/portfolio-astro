<template>
  <ExperienceBlock v-for="workItem in workExperience" @toggleDescription="toggleDescription" :work-item="workItem" :key="workItem.id"/>
</template>
<script>
import ExperienceBlock from './ExperienceBlock.vue';
import constants from '../constants';

export default {
    data() {
        return {
            workExperience: constants.workExperience.map(item => ({ ...item, isVisible: false })).reverse()
        };
    },
    methods: {
        toggleDescription(id) {
            this.workExperience = this.workExperience.map(item => ({ ...item, isVisible: item.id === id ? !item.isVisible : false }));
        }
    },
    components: { ExperienceBlock }
}
</script>