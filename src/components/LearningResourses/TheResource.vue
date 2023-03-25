<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12">
        <div class="text-center">
          <base-button
            @click="setSelectedTab('stored-resources')"
            style="min-width: 11rem"
            :class="selectedTab === 'stored-resources' ? 'active' : null"
            >Stored Resources</base-button
          >
          <base-button
            @click="setSelectedTab('add-resource')"
            style="min-width: 11rem"
            :class="selectedTab === 'add-resource' ? 'active' : null"
          >
            Add Resource</base-button
          >
        </div>
      </div>
    </div>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import storedResources from "./storedResources.vue";
import AddResource from "./AddResource.vue";

export default {
  components: {
    storedResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "official-guide",
          title: "Official Guide",
          description: "The official Vue js description",
          link: "https://vuejs.org",
        },
        {
          id: "official-guide 2",
          title: "Official Guide 2",
          description: "The official Vue js description 2",
          link: "https://vuejs.org",
        },
        {
          id: "official-guide 3",
          title: "Official Guide 3",
          description: "The official Vue js description 3",
          link: "https://vuejs.org",
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource
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
      this.selectedTab = "stored-resources";
    },

    deleteResource(id){
      const idx = this.storedResources.findIndex(res => res.id === id)
      this.storedResources.splice(idx,1)
      // this.storedResources = this.storedResources.filter((r)=>{ return r.id !== id})
      // console.log(this.storedResources)
    }
  },
};
</script>
