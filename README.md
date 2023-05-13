### app name:  plan-vue
### Live site: https://project-tracker-vue.netlify.app/

### vue create my-app
### how to create a mock server:

create a folder named db in root and create a file named db.json and paster some json data:
```
install: npm i json-server      
in terminal: npx json-server --watch data/db.json 
```
```
Now connect it:
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
```  
### Install and use Bootstrap5:
```
npm i bootstrap
```
```
in main.js:
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.bundle.js'
```
GET API:
```
  data() {
    return {
      projects: [],
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
```
POST API:
```
<form @submit.prevent="handleSubmit">
        <label>Title</label>
        <input type="text" v-model="title" required/>
        <label>Details</label>
        <textarea v-model="details" required></textarea>
        <button>Add Project</button>
</form>
    
methods: {
    handleSubmit(){
        let project = {
            title : this.title,
            details : this.details,
            complete: false
        }
        fetch('http://localhost:3000/projects', {
            method: "POST",
            headers: { 'Content-Type': 'application/json'},
            body: JSON.stringify(project)
        }).then(()=>{
            this.$router.push('/')
        }).catch(err => err.message)
    }
   }
```
PATCH API:
```
<form @submit.prevent="handleSubmit">
      <label>Title:</label>
      <input type="text" v-model="title" required/>
      <label>Details:</label>
      <textarea v-model="details" required></textarea>
      <button>Update Project</button>
  </form>
  ```
  ```
  data(){
    return {
      title: '', 
      details: '',
      uri: 'http://localhost:3000/projects/' + this.id
    }
  methods: {
    handleSubmit() {
        // let project = {
        //     title : this.title,
        //     details : this.details,
        //     complete: false
        // }
        fetch(this.uri, {
            method: "PATCH",
            headers: { 'Content-Type': 'application/json'},
            body: JSON.stringify({title: this.title, details: this.details})
        }).then(()=>{
            this.$router.push('/')
        }).catch(err => err.message)
    }
  }
```
DELETE API:
```
<span @click="deleteProject" class="material-icons">delete</span>
```
```
data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id,
    };
  },

  methods: {
    deleteProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.project.id))
        .catch(err => console.log(err))
    },
```    

