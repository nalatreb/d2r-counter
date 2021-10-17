<template>
  <v-app>
    <v-app-bar
      app
      dark
    >
      <v-app-bar-title>D2R Counter</v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn @click="reset()">
        Reset
      </v-btn>

      <v-btn @click="save()">
        Save
      </v-btn>

      <v-btn @click="openBrowser()">
        Load
      </v-btn>

      <input @change="load()" type="file" id="file-load" accept="application/json" style="display:none">

    </v-app-bar>

    <v-main>
      <HelloWorld :bosses="bosses"/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import bosses from './assets/boss_template.json'

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    bosses,
    loadedBosses: bosses
  }),
  methods: {
    async save() {
      const fileHandle = await window.showSaveFilePicker();
      const fileStream = await fileHandle.createWritable();
      await fileStream.write(new Blob([JSON.stringify(this.bosses)], {type: 'application/json'}));
      await fileStream.close();
    },
    openBrowser() {
      const file = document.getElementById('file-load');
      file.click();
    },
    load() {
      const file = document.getElementById('file-load').files[0];
      const reader = new FileReader();
      reader.onload = (event) => {
        this.bosses = JSON.parse(event.target.result);
        this.loadedBosses = JSON.parse(event.target.result);
      }
      reader.readAsText(file);
    },
    reset() {
      this.bosses = JSON.parse(JSON.stringify(this.loadedBosses));
    }
  },
};
</script>
