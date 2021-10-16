<template>
  <v-container fluid>
    <v-row dense>
      <v-col
          v-for="boss in bosses"
          v-bind:key="boss.id"
      >
        <v-card
            class="mx-auto"
            max-width="400"
        >
          <v-img
              class="white--text align-end"
              height="200px"
              :src="boss.image"
          >
            <v-card-title>{{ boss.name }}</v-card-title>
          </v-img>

          <v-card-text class="text--primary">
            <v-simple-table>
              <template v-slot:default>
                <tbody>
                <tr v-for="difficulty in boss.difficulties" v-bind:key="difficulty.id">
                  <td>{{ difficulty.text }}</td>
                  <td>{{ difficulty.count }}</td>
                  <td>
                    <v-btn
                        class="mx-2"
                        fab
                        dark
                        x-small
                    >
                      <v-icon dark @click="increase(boss.id, difficulty.id)">
                        mdi-plus
                      </v-icon>
                    </v-btn>
                  </td>
                </tr>
                </tbody>
              </template>
            </v-simple-table>
          </v-card-text>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import bosses from '../assets/boss_template.json'

  export default {
    name: 'HelloWorld',

    data: () => ({
      bosses
    }),
    methods: {
      increase(bossId, difficultyId) {
        console.log(bossId, difficultyId);
        const boss = this.bosses.filter(boss => boss.id === bossId).pop();
        boss.difficulties.filter(difficulty => difficulty.id === difficultyId).pop().count += 1;
      }
    }
  }
</script>
