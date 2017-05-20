<template>
<form>
    <input type=submit @click="toggleEdit" :value=editLabel></input>
    <div v-if="edit">
        <input v-model="date"/>
   </div>
    <div v-else>
        {{renderedDate}}
    </div>
</form>
</template>

<script>

function fakeGetData (d) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(new Date(d).toString())
        }, 500)
    })
}

export default {
    data () {
        return {
            warning: true,
            date: '1979-01-03',
            renderedDate: null,
            edit: false
        }
    },
    mounted () {
        this.renderedDate = 'initial not formatted'
    },
    watch: {
        date: function () {
            this.renderDate()
        }
    },
    computed: {
        editLabel: function () {
            return this.edit ? 'Save' : 'Edit'
        }
    },
    methods: {
        toggleEdit () {
            this.edit = !this.edit
        },
        renderDate () {
            let self = this
            fakeGetData(this.date).then(function (text) {
                self.renderedDate = text
            })
        }
    }
}
</script>

<style>
    body {
        color: blue;
    }
</style>
