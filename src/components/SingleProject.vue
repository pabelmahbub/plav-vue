<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions" @click="showDetails = !showDetails">
      <h3>{{ project.title }}</h3>

      <div class="icons">
        <router-link :to=" '/projects/' + project.id">
          <span class="material-icons">edit</span>
        </router-link>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="toggleComplete" class="material-icons tick">done</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
// const id = this.$route.params.id
export default {
  props: ['project'],
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
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
      }).then(() => {
        this.$emit('complete', this.project.id)
      }).catch(err => console.log(err))
    }
  }
  
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  border-left:6px solid tomato
}

h3 {
  cursor: pointer;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover{
  color:#777;
  font-size: 27pxx;
}

.project.complete {
  border-left: 6px solid #00ce89;
}

.project.complete .tick {
  color: #00ce89;
}
</style>
