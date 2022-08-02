<template>
    <div class="project">
        <div class="action">
            <h3 @click="this.showDetails = !this.showDetails">{{ prop.title }}</h3>
            <div class="icons">
                <span @click="changeComplete" class="material-icons" >done</span>
                <span class="material-icons" @click="deleteItem">delete</span>
                <span class="material-icons" >edit</span>
            </div>
        </div>
        <div v-if="showDetails" class="details">
            {{ prop.details }}
        </div>
    </div>
</template>

<script>
export default {
    props: ['prop'],
    data() {
        return {
            showDetails: false,
            uri: 'http://localhost:3000/jsonproject/' + this.prop.id
        }
    },
    methods: {
        deleteItem() {
            fetch(this.uri, { method: "DELETE" })
                .then(() => this.$emit('deleteFromHomeProject', this.prop.id))
                .catch(err => console.log(err.message))
        }
    },
    changeComplete(){
            fetch(this.uri, {
                    method: 'PATCH',
                    headers:{'Content-Type' : 'application/json'},
                    body: JSON.stringify({complete: !this.prop.complete}) })
                    .then(() => this.$emit('completeChanger', this.prop.id))
                    .catch(err => console.log(err.message))

                    // body: JSON.stringify({complete: !this.prop.complete ==> this two complete come from db.json
                
        }
}
</script>

<style>
.project {
    margin: 35px auto;
    padding: 10px 10px 15px 25px;
    border: 2px;
    border-radius: 3px;
    background: rgb(224, 220, 238);
    box-shadow: 2px 3px 4px rgba(28, 5, 5, 0.5);
    text-align: left;
    border-left: 4px solid;
}

.action {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h3 {
    cursor: pointer;
}

.material-icons {
    padding: 0 3px;
    font-size: 24px;
    color: #777;
    cursor: pointer;
}

.material-icons:hover {
    color: rgb(105, 79, 79);
}
</style>