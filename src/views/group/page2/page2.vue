<template>
    <Table height="200" :columns="columns1" :data="data2"></Table>
</template>
<script>
    export default {
    	 name: 'page2',
        data () {
            return {
                columns1: [
                    {
                        title: 'Name',
                        key: 'name'
                    },
                    {
                        title: 'Age',
                        key: 'age'
                    },
                    {
                        title: 'Address',
                        key: 'address'
                    }
                ],
                data2: [
             
                ]
            }
        }
    }
</script>


