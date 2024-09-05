<template>
    <div id="app">
        <rich-select v-model="selectedDatasource" :options="datasourceOptions"></rich-select>
    </div>
</template>

<script>
import RichSelect from './components/RichSelect'

import mysqlLogo from '@/assets/images/mysql_logo.svg'
import sqlServerLogo from '@/assets/images/sql_server_logo.svg'
import postgresLogo from '@/assets/images/postgresql_logo.svg'
import oracleLogo from '@/assets/images/oracle_logo.svg'
import esLogo from '@/assets/images/elasticsearch_logo.svg'
import prometheusLogo from '@/assets/images/prometheus_logo.svg'
import influxdbLogo from '@/assets/images/influxdb_logo.svg'

export default {
    name: 'App',
    components: {
        RichSelect
    },
    data () {
        return {
            datasourceOptions: [
                {
                    key: '1',
                    label: 'MySQL-1',
                    type: 'MySQL',
                    icon: mysqlLogo
                },
                {
                    key: '2',
                    label: 'SQL Server-2',
                    type: 'SQL Server',
                    icon: sqlServerLogo
                },
                {
                    key: '3',
                    label: 'PostgresSQL-3',
                    type: 'PostgresSQL',
                    icon: postgresLogo
                },
                {
                    key: '4',
                    label: 'Oracle-4',
                    type: 'Oracle',
                    icon: oracleLogo
                },
                {
                    key: '5',
                    label: 'Elasticsearch-5',
                    type: 'Elasticsearch',
                    icon: esLogo
                },
                {
                    key: '6',
                    label: 'Prometheus-6',
                    type: 'Prometheus',
                    icon: prometheusLogo
                },
                {
                    key: '7',
                    label: 'influxdb-7',
                    type: 'influxDB',
                    icon: influxdbLogo
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
