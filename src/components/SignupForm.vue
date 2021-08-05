<template>
  <form>
    <label> Email:</label>
    <input type="email" v-model="email" required />
    <label> Password:</label>
    <input type="password" v-model="password" required />
    <label>Role:</label>
    <select v-model="role">
      <option value="developer"> Web Developer </option>
      <option value="designer"> Web Designer </option>
    </select>

    <label> Skills: </label>
    <input type="text"  v-model="tempSkill" @keyup="addSkill" placeholder="use ',' to separate your skills ">
    <div v-for=" skill in skills" :key="skill" class="pill" >
      <span @click="deleteSkill(skill)" > {{skill}}</span>
    </div>
    
    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label> Accept terms and conditions </label>
    </div>



    <div>
     <p> Add interests </p>
      <input type="checkbox" value="sports" v-model="names" />
      <label> Sports </label>
    </div>
    <div>
      <input type="checkbox" value="food" v-model="names" />
      <label> Food </label>
    </div>
    <div>
      <input type="checkbox" value="travel" v-model="names" />
      <label> Travel </label>
    </div>

    <div class="submi">
      <button> Create an account </button>
    </div>
  </form>
  <p>your email: {{ email }}</p>
  <p>your password: {{ password }}</p>
  <p>your role: {{ role }}</p>
  <p>Accepted terms and conditions: {{ terms }}</p>
  <p>Names: {{ names }}</p>
  <p>skills: {{ skills }}</p>
</template>

<script>
export default {
  name: "SignupForm",
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      names: [],
      tempSkill: '',
      skills: []
    };
  },

  methods: {
    addSkill(e) {
      if(e.key === ","  && this.tempSkill) {
        const newTempSkill = this.tempSkill.replace(',', '')
        if(newTempSkill !== '' && newTempSkill !== ','  ) {
        const skillToUpperCase = newTempSkill.toUpperCase()
        if(!this.skills.includes(skillToUpperCase)) {
          this.skills.push(skillToUpperCase)
        }
        this.tempSkill = ''
        }
      }
    },

    deleteSkill(skill) {
     this.skills = this.skills.filter(el=> el !== skill)

    }
  }
};
</script>

<style scoped>
form {
  max-width: 420px;
  margin: 30px auto;
  background-color: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #4b4b4b;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
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
margin: 20px 10px 0 0 ;
padding: 6px 12px ;
background-color: #eee;
border-radius: 20px;
font-size: 12px;
letter-spacing: 1px;
font-weight: bold;
color: #777;
cursor: pointer;
}

button{
  background-color: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;

  }
.submit{
  text-align: center;
}
</style>
