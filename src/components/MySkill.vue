<template>
  <div>
    {{ name }}
    <button>Change Name</button>

    <div v-bind:class="{alert :showAlert, another_class :showAlert}"></div>
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="EnterSkill" v-model="st" >
    </form>
    <transition-group name="list" enter-active-class="animated flipInx" leave-active-class="animated flipOutx">
      <ul>
        <li v-for="(data, index) in skills" :key="index">{{ index }}. {{ data.skill }} </li>
      </ul>
    </transition-group>
    <p>{{ st }}</p>
  </div>
</template>

<script>
export default {
  name: 'MySkill',
  data () {
    return {
      name: 'Push_Button',
      btnState: true,
      skills: [{ skill: 'Vue.js' }, { skill: 'Json.js' }],
      showAlert: true,
      st: ''
    }
  },
  methods: {
    addSkill () {
      this.skills.push({ skill: this.st })
      this.st = ''
    }
  }

}

</script>
<style src = "./style.css" scoped>

</style>
