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
    <keep-alive>
        <component :is="selectedTab"> </component>
    </keep-alive>
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
                    id: 'vue-doc',
                    title: 'Vue.js: The Documentary',
                    description: 'History of the framework creation',
                    link: 'https://youtu.be/OrxmtDw4pVI',
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.deleteResource,
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
        addResource(title, description, link) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link,
            };

            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        deleteResource(resId) {
            const resIndex = this.storedResources.findIndex(
                (res) => res.id === resId
            );
            this.storedResources.splice(resIndex, 1);
        },
    },
};
</script>
