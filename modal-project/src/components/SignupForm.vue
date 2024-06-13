<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input class="signInput" type="email" required v-model="email">

    <label>Password:</label>
    <input class="signInput" type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role</label>
    <select v-model="role">
      <option value="frontend">Frontend Developer</option>
      <option value="backend">Backend Developer</option>
    </select>

    <label>Skills:</label>
    <input class="signInput" type="text" v-model="tempSkill" @keyup="addSkill">
    <div class="pill" v-for="skill in skills" :key="skill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required>
      <label>Accept term and conditions</label>
    </div>

    <div>
      <input type="checkbox"  v-model="names" value="full-time">
      <label>Full Time</label>
    </div>
    <div>
      <input type="checkbox"  v-model="names" value="part-time">
      <label>Part Time</label>
    </div>
    <div>
      <input type="checkbox"  v-model="names" value="contract">
      <label>Contract</label>
    </div>

    <div class="submit">
      <button>Create An Account</button>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
  <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: 'example@email.com',
      password: 'example password',
      role: '',
      terms: false,
      names: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ',' && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill.slice(0, -1))) {
          this.skills.push(this.tempSkill.slice(0, -1))
        }
        
        this.tempSkill = ''
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handleSubmit() {
      // Validate password
      this.passwordError = this.password.length > 5 ? 
      '' : 'Password must be at least 6 chars long'

      if (!this.passwordError) {
        console.log('Good!')
      }
    }
  }
}
</script>

<style>
  form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    /* font-size: 0.6em; */
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }

  .signInput, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }

  input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }

  .pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }

  .submit {
    text-align: center;
  }

  .error {
    color: red;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
</style>