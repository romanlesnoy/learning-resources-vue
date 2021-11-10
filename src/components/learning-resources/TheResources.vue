<template>
    <base-card>
        <base-button
            @click="setSelectedtab('stored-resources')"
            :mode="storedResButtonMode"
            >Stored Recources</base-button
        >
        <base-button
            @click="setSelectedtab('add-resource')"
            :mode="addResButtonMode"
            >Add Recources</base-button
        >
    </base-card>
    <component :is="selectedTab"> </component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
    components: {
        StoredResources,
        AddResource,
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Google',
                    link: 'https://google.com',
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resources' ? null : 'flat';
        },
    },
    methods: {
        setSelectedtab(tab) {
            this.selectedTab = tab;
        },
    },
};
</script>
