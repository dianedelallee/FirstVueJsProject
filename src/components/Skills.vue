<template>
  <div class="hello">
    <h1>{{ title }}</h1>

    <div class="holder">
      <span>These are your skills</span>

      <form @submit.prevent="addSkill">
        <input
          type="text"
          placeholder="Enter a new skill"
          v-model="skill"
          v-validate="'min:5'"
          name="skill"
        >

        <transition
          name="alert-in"
          enter-active-class="animated shake"
          leave-active-class="animated flipOutX"
        >
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>
      </form>
      <ul>
        <transition-group
          name="list"
          enter-active-class="animated bounceInUp"
          leave-active-class="animated bounceInDown"
        >
          <li v-for="(data, index) in skills" :key="index">
            {{ data.skill }}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      title: "Diane",
      skill: "",
      skills: [{ skill: "Vue.js" }, { skill: "Frontend Developer" }]
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = "";
        }
      });
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Skills.css" scoped>
</style>
