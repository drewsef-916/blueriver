<template>
  <div>
      <div class="zone-group" v-for="(buildingZone, index) in buildingsByZone" :key="buildingZone.index">
        <h3>{{ buildingZoneNames[index] }}</h3>
        <ul>
          <li v-for="building in buildingZone" :key="building.buildingname">
            <a v-if="building.black == 0" href="https://applefacilities.review.blueriver.com">
              {{ building.buildingname }}
            </a>
            <span v-else>
              {{ building.buildingname }}
            </span>
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
import buildingJson from '@/assets/buildingData.json'

export default {
  name: 'BuildingIndex',
  data: function() {
    return {
      buildings: buildingJson.data.items,
      buildingZoneNames: [],
      buildingsByZone: []
    }
  },
  methods: {
    getBuildingsByZone() {
      const zones = this.buildings.slice().map(bldg => bldg.buildingzone);
      const [...zonesSet] = new Set(zones);
      const sortedZones = zonesSet
        .filter(elem => elem !== "Other Bay Area")
        .sort()
        .slice(0)
      const other = sortedZones.push("Other Bay Area");
      sortedZones.forEach(zone => { 
        let byZone = this.buildings
          .slice()
          .filter(bldg => bldg.buildingzone === zone)
          .sort((a,b) => a.buildingname - b.buildingname);
        console.log(byZone);
        this.buildingZoneNames.push(zone);
        this.buildingsByZone.push(byZone);
      })
    },
    // getBuildingData: function() {
    //   axios.get('https://applefacilities.review.blueriver.com/index.cfm/_api/json/v1/scv/building/?andOpenGrouping&locationCode%5B0%5D=sqo&or&locationCode%5B2%5D=nwr&or&locationCode%5B4%5D=scv&or&locationCode%5B6%5D=sfo&closeGrouping&fields=buildingname,buildingabbr,lat,lng,black,buildingZone&active=1&cachedwithin=600')
    //   .then(res => this.buildings = res.data.items)
    //   .catch(err => console.log(err));
    // },
    // getBuildingJson: function() {
    //   this.buildings = buildingJson.data.items
    // },
  },
  created() {
    this.getBuildingsByZone();
  }
}
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  color: #333;
}
a {
  color: #42b983;
}
</style>
