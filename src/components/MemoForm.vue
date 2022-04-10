<template>
  <div><input type="text" v-model="title"></div>
  <div><textarea v-model="content"></textarea></div>
  <div class="center">
    <button @click="save">保存</button>
    <button @click="remove" v-if="memo.id">削除</button>
  </div>
</template>

<script>
export default {
    name: 'MemoForm',
    props: [
        'memo'
    ],
    data() {
        return {
            title: this.memo.title,
            content: this.memo.content
        }
    },
    methods: {
        save() {
            let memo = {
                title: this.title,
                content: this.content
            }

            if (this.memo.id) {
                memo.id = this.memo.id
            }

            this.$store.commit('save', memo)
            this.$router.push('/')
        },
        remove () {
            this.$store.commit('delete', this.memo.id)
            this.$router.push('/')
        }
    }
}
</script>

<style scoped>
div {
    margin-bottom: 10px;
}
input[type=text] {
    width: 100%;
}
textarea {
    width: 100%;
    height: 30em;
}
button {
    width: 5em;
    margin: 3px;
}
.center {
    text-align: center;
}
</style>