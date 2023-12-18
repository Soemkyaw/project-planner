<template>
  <form @submit.prevent="addProject">
    <label>Title</label>
    <input type="text" v-model="title">
    <label>Detail</label>
    <input type="text" v-model="detail">
    <button>Create Project</button>
  </form>
</template>

<script>
export default {
    data() {
        return {
            title: "",
            detail: ""
        }
    },
    methods: {
        addProject() {
            fetch("http://localhost:3000/projects", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    title: this.title,
                    detail: this.detail,
                    complete: false
                })
            })
                .then(() => {
                    this.$router.push({name:'home'})
                })
                .catch((err) => {
                    console.log(err);
                })
        }
    },
}
</script>

<style>
    form{
        background-color: rgb(246, 242, 242);
        padding: 40px;
        /* text-align: center; */
    }
    form label{
        display: inline-block;
        margin: 10px 0;
        font-weight: bold;
        letter-spacing: 1px;
        text-transform: uppercase;
        color: #b0a7a7;
    }
    input{
        display: block;
        width: 100%;
        padding: 15px;
        margin-bottom: 20px;
        border: none;
        background-color: rgb(246, 242, 242);
        border-bottom: 1px solid #aaa;
        color: #555;
    }
    button{
        display: block;
        margin: 0px auto;
        margin-top: 30px;
        border: none;
        padding: 15px;
        background-color: #30e3ca;
        border-radius: 6px;
    }
</style>