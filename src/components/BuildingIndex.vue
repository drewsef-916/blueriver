<template>
  <div>
    <ul>
      {{ sortBuildings.buildingname }}
    </ul>
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
      sortedBuildings: [],
      buildingsByZone: []
    }
  },
  methods: {
    // getBuildingData: function() {
    //   axios.get('https://applefacilities.review.blueriver.com/index.cfm/_api/json/v1/scv/building/?andOpenGrouping&locationCode%5B0%5D=sqo&or&locationCode%5B2%5D=nwr&or&locationCode%5B4%5D=scv&or&locationCode%5B6%5D=sfo&closeGrouping&fields=buildingname,buildingabbr,lat,lng,black,buildingZone&active=1&cachedwithin=600')
    //   .then(res => this.buildings = res.data.items)
    //   .catch(err => console.log(err));
    // },
    // getBuildingJson: function() {
    //   this.buildings = buildingJson.data.items
    // },
    sortByBuildingZone: function() {
      // const zoneList = [];
      // const zoneGroups = [];
      // console.log(sortedBuildings);
      // this.buildings.forEach(building => {
      //   if (!zoneList.includes(building.buildingzone)) zoneList.push(building.buildingzone)
      // });

      // this.buildingZones = zoneList;
    }
  },
  computed: {
    sortBuildings() {
      return this.buildings.sort((a,b) => a.buildingname - b.buildingname);
    }
  },
  created() {
    this.sortByBuildingZone();
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
}
a {
  color: #42b983;
}
</style>
