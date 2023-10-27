<template>
  <div class="p-3 w-80 text-teal-50 bg-gradient-to-r from-teal-800 to-teal-400 border-2 border-slate-900" :class="{'h-28':!workItem.isVisible, 'h-auto':workItem.isVisible}">
    <h3>{{workItem.companyName}}</h3>
    <h4 class="text-sm">{{workItem.period}}</h4>
    <div class="flex justify-center my-2">
      <button class="my-2" @click="toggleDescription" :class="{more:!workItem.isVisible, less:workItem.isVisible}"></button>
    </div>
    <div v-if="workItem.isVisible" id="description-container">
      <ul class="ml-5 mb-4">
        <li class="list-disc w-4/5" v-for="(item, index) in workItem.description" :key="index">{{ item }}</li>
      </ul>
      <section>
        <p>Tech Stack:</p>
        <p>{{workItem.techStack}}</p>
      </section>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    workItem: {
      companyName: String,
      period: String,
      description: [String],
      techStack: String,
      isVisible: Boolean,
      id:Number | String
    }
  },
  data() {
    return {
      isDescriptionVisible: false
    }
  },
  methods: {
    toggleDescription(){
      return this.$emit('toggleDescription',this.workItem.id)
    }
  },
  emits: ['toggleDescription']
}
</script>

<style>
  button.more {
    border-right: 3px solid white;
    border-bottom: 3px solid white;
    width: 1em;
    height: 1em;
    transform: rotate(45deg);
  }
  button.less {
    border-right: 3px solid white;
    border-bottom: 3px solid white;
    width: 1em;
    height: 1em;
    transform: rotate(-135deg);
  }
  button.more:hover {
    animation: bounce 0.8s infinite ease-in-out;
  }
  button.less:hover {
    animation: bounce-back 0.8s infinite ease-in-out;
  }

  @keyframes bounce {
    0% {
      transform: translateY(0) rotate(45deg);
    }
    50% {
      transform: translateY(5px) rotate(45deg);
    }
    100% {
      transform: translateY(0) rotate(45deg);
    }
  }
  @keyframes bounce-back {
    0% {
      transform: translateY(0) rotate(-135deg);
    }
    50% {
      transform: translateY(5px) rotate(-135deg);
    }
    100% {
      transform: translateY(0) rotate(-135deg);
    }
  }
</style>