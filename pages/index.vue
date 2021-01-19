<!-- I will be adding notes for me to remember -->
<template>
  <v-container fluid class="pa-0">
    <v-sheet height="520px" color="red lighten-4">
      <v-row align="center" class="pa-12 black--text">
        <v-col>
          <span style="font-size: 62px" class="text-uppercase">Price List</span>
          <p style="font-size: 24px; max-width: 640px">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Velit ea
            aperiam eveniet sunt sed, nam non et nesciunt nihil, necessitatibus
            facilis libero, corporis maxime voluptates veniam ipsa perferendis
            vero itaque.
          </p>
        </v-col>
      </v-row>
    </v-sheet>
<template>
      <v-container fluid class="white">
        <div class="tabs d-none d-sm-flex">
          <div
            class="tab-item text-uppercase"
            @click="tab = index"
            :class="{ active: tab === index }"
            v-for="(item, index) in items"
            :key="index"
          >
            {{ item.tab }}
          </div>
        </div>
        <v-sheet color="white" height="5px"></v-sheet>
      </v-container>
      <v-container fluid class="grey">
        <v-container class="white">
          <v-tabs-items
            v-model="tab"
          >
            <v-card color="#B4161B" class="text-center justify-center">
              <v-tab-item
                class="text-uppercase"
                style="font-size: 35px"
                v-for="(item, index) in items"
                :key="index"
              >
                {{ item.tab }}
              </v-tab-item>
            </v-card>
          </v-tabs-items>
          <v-row
            class="tab-content d-none d-sm-flex"
            v-for="(item, index) in items"
            :key="index"
          >
            <template v-if="tab === index">
              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>
                    <div
                      class="black--text"
                      v-for="(content, index) in item.content"
                      :key="index"
                    >
                      <p class="text-uppercase text-left">
                        <v-row>
                          <v-col cols="3" style="font-size: 25px" class="font-weight-black">
                            {{ content.name }}
                          </v-col>                    
                          <v-col cols="9">                    
                            <v-simple-table dense light>
                              <template>
                                <tbody>
                                  <tr                                    
                                    v-for="item in items"
                                    :key="item.tab"
                                  >
                                    <td>{{ item.tab }}</td>
                                    <td>{{ item.tab }}</td>
                                  </tr>
                                </tbody>
                              </template>
                            </v-simple-table>
                          </v-col>
                        </v-row>
                      </p>
                    </div>
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </template>
          </v-row>
        </v-container>
      </v-container>
    </template>
  </v-container>
</template>

<script>
import PaymentCalculator from "@/components/home/PaymentCalculator";

import { mapGetters } from "vuex";
export default {
  components: {
    PaymentCalculator,
  },
  data() {
    return {
      tab: 0,
      items: [
        { tab: "Cars", content: null },
        { tab: "Vans & Trucks", content: null },
        { tab: "SUVS", content: null },
      ],
      showCalc: false,
    };
  },
  methods: {
    addContent() {
      this.items.forEach((el) => {
        if (el.tab == "Cars") el.content = this.cars;
        if (el.tab == "Vans & Trucks") el.content = this.van_trucks;
        if (el.tab == "SUVS") el.content = this.suvs;
      });
    },
    linkTo(route) {
      this.$router.push(route);
    },
  },
  computed: {
    ...mapGetters("vehicles", ["all", "cars", "van_trucks", "suvs"]),
  },
  created() {
    this.addContent();
  },
};
</script>

<style lang="scss" scoped>
.vehicle-chooser {
  margin: 0;
  padding: 0;
}

.tabs {
  display: flex;
  justify-content: space-around;
  // padding: 0.5rem 0;
  margin: 0 auto;
  border-bottom: 1px solid black;
  max-width: 500px;

  .tab-item {
    color: black;
    font-size: 20px;
    cursor: pointer;

    &:hover {
      color: #c3002f;
    }

    &.active {
      font-weight: 600;
      border-bottom: 4px solid #342e37;
    }
  }
}

.tab-content {
  color: black;
  margin: 0 100px;
  display: flex;
  justify-content: space-evenly;

  .content-item {
    p {
      text-align: center;
      font-weight: 600;
    }

    &:hover {
      color: #c3002f;
      cursor: pointer;
    }
  }
}

.car-card {
  position: relative;

  .car {
    position: absolute;
    left: -30px;
    bottom: 15%;
  }
}
</style>
