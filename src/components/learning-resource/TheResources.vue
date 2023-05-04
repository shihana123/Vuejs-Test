<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResModeButton"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResModeButton"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive><component :is="selectedTab"></component></keep-alive>
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
          id: 'first-resource',
          title: 'First Resource',
          description: 'This is the first resource',
          link: 'http://firstexample.com',
        },
        {
          id: 'second-resource',
          title: 'Second Resource',
          description: 'This is the second resource',
          link: 'http://secondexample.com',
        },
      ],
    };
  },
  computed: {
    storedResModeButton() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResModeButton() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource
    };
  },
  methods: {
    setSelectedTab(tab) {
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
    removeResource(resId){
        const resIndex = this.storedResources.findIndex(res => res.id === resId);
        this.storedResources.splice(resIndex,1);
    }
  },
};
</script>
