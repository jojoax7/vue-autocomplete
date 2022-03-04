<template>
    <div
        id="app"
        class="container mx-auto mt-10 px-10"
    >
        <div class="mx-auto mt-20">
            <h3 class="text-center text-lg font-bold mb-4">
                Vue.js autocomplete
            </h3>
            
            <div class="w-64 mx-auto">
                <Autocomplete 
                    v-model="client"
                    :options="clients"
                    value-key="id_client"
                    label-key="label"
                    placeholder="Search client"
                    @shouldSearch="searchClients"
                    @select="onSelect"
                />
            </div>
        </div>
    </div>
</template>

<script>
    import Autocomplete from '@/components/Autocomplete';

    export default {
        name: 'App',

        components: {
            Autocomplete,
        },

        data() {
            return {
                client: '',
                clients: [],
            };
        },

        methods: {
            searchClients(query) {
                fetch(`http://localhost:8000/api/clients?term=${query}`).then(response => response.json()).then((r) => {
                    this.clients = r.data;
                });
            },
            onSelect(city) {
                console.log(city);
            },
        },
    };
</script>
