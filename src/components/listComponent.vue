<template>
    <div>
        <ul v-for="(item, gIndex) in list" :key="gIndex">
            <li>
                {{ item.title }}
            </li>
            <ul v-for="(subItem, index) in item.subList" :key="index">
                <li>
                    {{ subItem }}
                </li>
            </ul>
        </ul>
        <hr>

        <ul v-for="(item, index)  in segment" :key="index">
            <li>{{ item }}</li>
        </ul>
        <button :disabled="pageNum <= 0" @click="prevPage">Назад</button>
        <button :disabled="pageNum >= pageAll" @click="nextPage">далі</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            list: [
                {
                    title: 'Список покупок №1',
                    subList: ['Хліб', 'Молоко', 'Борошно']
                },
                {
                    title: 'Список покупок №2',
                    subList: ['Чай', 'Вода', 'Печіво']
                },
                {
                    title: 'Список покупок №3',
                    subList: ['Сік', "М'ясо", 'Салат']
                }
            ],
            pageNum: 0,
            listData: '',
            size: 4

        }
    },
    methods: {
        createFakeData() {
            let data = [];
            for (let i = 0; i < 36; i++) {
                data.push('Номер ' + (i + 1));
            }
            return this.listData = data;
        },
        nextPage() {
            this.pageNum++;
        },
        prevPage() {
            this.pageNum--;
        },
    },
    mounted() {
        this.createFakeData();
    },
    computed: {
        segment() {
            const start = this.pageNum * this.size,
                end = start + this.size;
            return this.listData.slice(start, end);
        },
        pageAll() {
            return Math.ceil(this.listData.length / this.size) - 1;
        },
    }
}
</script>