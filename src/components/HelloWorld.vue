<template>
  <div class="hello" v-if="launches">
    <h1>Space X Launches</h1>
    <h4 v-for="launch in launches.launches" :key="launch.id">
      {{ launch.mission.name }}
      {{ launch.rocket.name }} : {{ launch.site }}
    </h4>
    <div>
      <h1>Your Task</h1>
      <h4>{{ pricing.sections[0].text }} ${{ pricing.dueOnCompletion }}</h4>
      <p>{{ pricing.sections[2].items[0].text }}</p>
      <h4>{{ pricing.sections[1].text }}</h4>
      <ul>
        <li v-for="include in pricing.sections[1].items" :key="include.id">
          {{ include.text }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      launches: null,
      pricing: null
    };
  },
  apollo: {
    launches: gql`
      {
        launches(pageSize: 5) {
          launches {
            site
            mission {
              name
            }
            rocket {
              name
              type
            }
          }
        }
      }
    `,
    pricing: gql`
      {
        pricing: prePriced {
          dueOnCompletion
          sections {
            items {
              text
            }
          }
        }
      }
    `
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  text-align: left;
  margin: 0 auto;
  display: inline-block;
}
a {
  color: #42b983;
}
</style>
