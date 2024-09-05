<template>
    <div id="app">
        <img-select v-model="selectedDatasource" :options="datasourceOptions"></img-select>
    </div>
</template>

<script>
import ImgSelect from './components/ImgSelect'

export default {
    name: 'App',
    components: {
        ImgSelect
    },
    data () {
        return {
            datasourceOptions: [
                {
                    key: '1',
                    label: 'MySQL-1',
                    type: 'MySQL',
                    icon: require('@/assets/images/mysql_logo.svg')
                },
                {
                    key: '2',
                    label: 'PostgresSQL-2',
                    type: 'PostgresSQL',
                    icon: require('@/assets/images/postgresql_logo.svg')
                },
                {
                    key: '3',
                    label: 'Oracle-3',
                    type: 'Oracle',
                    icon: require('@/assets/images/oracle_logo.svg')
                },
                {
                    key: '4',
                    label: 'Elasticsearch-4',
                    type: 'Elasticsearch',
                    icon: require('@/assets/images/elasticsearch_logo.svg')
                },
                {
                    key: '5',
                    label: 'Prometheus-5',
                    type: 'Prometheus',
                    icon: require('@/assets/images/prometheus_logo.svg')
                },
                {
                    key: '6',
                    label: 'influxdb-6',
                    type: 'influxDB',
                    icon: require('@/assets/images/influxdb_logo.svg')
                }
            ],
            selectedDatasource: {}
        }
    },
    methods: {
        clickOk () {
            console.log(this.selectedDatasource.label)
            console.log(this.selectedDatasource.type)
        }
    }
}
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
    margin-left: 60px;
}
</style>
