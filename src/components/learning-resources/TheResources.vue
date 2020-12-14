<template>
  <base-card>
    <!-- When you add props or event listeners on custom components, by default they "fall through" to the root-level element in that custom component's template, which in this case is button element -->
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
  </base-card>
  <!-- Dynamic component -->
  <component :is="selectedTab"></component>
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
      // providing resources to all lower-level components
      resources: this.storedResources
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
    }
  }
}
</script>