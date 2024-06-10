<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
    >
      My Website Link</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
    >
      Add Website</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>
<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";
import BaseButton from "../UI/BaseButton.vue";
export default {
  components: {
    StoredResources,
    AddResource,
    BaseButton,
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "my-website",
          title: "My Website",
          description:
            "My personal website created in react and typescript with Node backend and mongoose database.",
          link: "https://bishalcarki.netlify.app/",
        },
        {
          id: "dance-school",
          title: "GrooveandVibe Dance School",
          description:
            "Website also created in react and Node backend with mongoose database.",
          link: "https://www.grooveandvibes.com.au/",
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
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
    removeResource(resId) {
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
      return this.selectedTab === "add-resource" ? null : "flat";
    },
  },
};
</script>
