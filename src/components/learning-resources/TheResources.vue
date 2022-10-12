<template>
  <base-card>
    <base-button
      @click="setselectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setselectedTab('add-resources')"
      :mode="addResButtonMode"
      >Add resources</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AddResources from "./AddResources.vue";

export default {
  components: { StoredResources, AddResources },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "official-version",
          title: "The Progressive JavaScript Framework",
          description:
            "An approachable, performant and versatile framework for building web user interfaces.",
          link: "https://vuejs.org/",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn with Google",
          link: "https://www.google.com",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.remoteResource,
    };
  },
  methods: {
    setselectedTab(tab) {
      this.selectedTab = tab;
      console.log(tab);
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },
    remoteResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "add-resources" ? null : "flat";
    },
  },
};
</script>
