<template>
  <base-card>
    <!-- When you add props or event listeners on custom components, by default they "fall through" to the root-level element in that custom component's template, which in this case is button element -->
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
  </base-card>
  <!-- Cache component so data is not lost when switching between tabs (for example inputted text) -->
  <!-- <component> is a dynamic component -->
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        { id: 'official-guide', title: 'Official Guide', description: 'The official Vue.js documentation.', link: 'https://vuejs.org' },
        { id: 'google', title: 'Google', description: 'Learn to Google...', link: 'https://google.com' },
      ]
    }
  },
  provide() {
    return {
      // Providing resources to all lower-level componentsn (provide/inject)
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource
    }
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description,
        link: url
      };
      this.storedResources.unshift(newResource);
      // Switch tab after new resource added
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      // Note - due to how provide/inject works, and since array is a reference type, can't replace whole array; will create a bug. Must manipulate existing array -> Vue recognizes this, and all components that injected this array will notice this as well
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  }
}
</script>