<template>
  <div class="container">
    <h1>VUE CRUD</h1>
     <form class="form">
      <input
        class="input"
        type="text"
        v-model="campaigName"
        placeholder="Enter Campaign Name"
        required
      />
      <input
        class="input"
        type="number" 
        v-model="bidAmount"
        placeholder="Bid amount" 
        required
       />
       <input
        class="input"
        type="number" 
        v-model="campaignFund"
        placeholder="Campaign Fund" 
        required
       />
      <select id="city" name="cities" v-model="city" class="input">
        <option value="">Choose a City</option>
        <option value="krakow">Kraków</option>
        <option value="warszawa">Warszawa</option>
        <option value="katowice">Katowice</option>
        <option value="sosnowiec">Sosnowiec</option>
      </select>
      <input
        class="input"
        type="number" 
        v-model="radius"
        placeholder="Radius" 
        required
      >
    </form>
    <button @click="addCampaign">
        SUBMIT
    </button>
    <table>
      <thead>
        <tr>
          <th>Campaig Name</th>
          <th>Bid amount</th>
          <th>Campaign Fund</th>
          <th>City</th>
          <th>Radius</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="campaign in campaigns" :key="campaign.id">
          <td contenteditable="true">{{campaign.name}}</td>
          <td contenteditable="true">{{campaign.bid}}</td>
          <td contenteditable="true">{{campaign.fund}}</td>
          <td contenteditable="true">{{campaign.city}}</td>
          <td contenteditable="true">{{campaign.radius}}</td>
          <td>
            <div @click="deleteTask(index)">
              <i class="icon-trash"></i>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
  @import '../crud.css';
  @import '../../fontello-6f68fb2f/css/fontello.css';
</style>

<script>
export default {
  name: "crud-app",
  props: {
    msg: String,
  },

  data() {
    return {
      id: 0,
      campaigName: "",
      bidAmount: "",
      campaignFund: "",
      city: "",
      radius: "",
      campaigns: [],
    };
  },

  methods: {
    getUniqueId(){
      return this.id++
    },

    deleteTask(index) {
      this.campaigns.splice(index, 1);
    },

    addCampaign() {
      if (this.campaigName.length === 0 | this.bidAmount.length === 0 | this.campaignFund.length === 0 | this.city.length === 0 | this.radius.length === 0)
       window.alert("fields cannot be empty");
      else {
        this.campaigns.push({
          id: this.getUniqueId(),
          name: this.campaigName,
          bid: this.bidAmount,
          fund: this.campaignFund,
          city: this.city,
          radius: this.radius,
        });
      }
      this.campaigName = "";
      this.bidAmount = "";
      this.campaignFund = "";
      this.city = "";
      this.radius = "";
    },
  },
};
</script>
