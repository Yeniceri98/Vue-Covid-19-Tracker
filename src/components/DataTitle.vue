<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{ title }}</h2>
        <!-- <div class="text-2xl mt-4 mb-10">{{ dataDate }}</div>   NOT: Yoruma aldık çünkü tarihin aşağıdaki gibi gözükmesini istiyoruz -->
        <div class="text-2xl mt-4 mb-10">{{ timestamp }}</div>
    </div>
</template>

<script>
import moment from 'moment'         // Tarihin daha güzel gözükebilmesi için bu kütüphaneyi indirdik https://yarnpkg.com/package/moment

export default {
    props: ['title', 'dataDate'],
    computed: {
        timestamp: function() {
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
        }
    }
}
</script>
