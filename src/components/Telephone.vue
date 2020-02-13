<template>
    <div class="mt-6">
        <input type="text" :placeholder="template" v-model="number" class="w-56 text-2xl bg-gray-300 p-3 rounded-lg focus:outline-none">
    </div>
</template>

<script>
    export default {
        name: "Telephone",

        props: [
          'template'
        ],
        data: function () {
            return {
                number: '',
                format: '',
                regex: '^',
            }
        },

        mounted() {
            let x = 1;

            this.format = this.template.replace(/X+/g, () => '$' + x++);

            this.template.match(/X+/g).forEach((char) => {

                //console.log(char.length);
                //console.log(key);

                this.regex += '(\\d{'+ char.length + '})?';

                //console.log(this.regex);

            });
        },

        watch: {
            number() {
                this.number = this.number.replace(/[^0-9]/g, '')
                    .replace(new RegExp(this.regex, 'g'), this.format)
                    .substr(0, this.template.length);
            }
        }
    }
</script>

<style scoped>

</style>
