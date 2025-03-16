<script setup>
import MiniStatisticsCard from "@/examples/Cards/MiniStatisticsCard.vue";
</script>
<template>
  <div class="py-4 container-fluid">

    <div class="row">
      <div class="col-lg-12">
        <div class="row">

          <div class="col-lg-3 col-md-6 col-12">
            <mini-statistics-card
              title="Events Sent"
              value="2300"
              description="<span
                class='text-sm font-weight-bolder text-success'
                >+550</span> since yesterday"
              :icon="{
                component: 'ni ni-button-play',
                background: 'bg-gradient-danger',
                shape: 'rounded-circle',
              }"
            />
          </div>

          <div class="col-lg-3 col-md-6 col-12">
            <mini-statistics-card
              title="Alerts"
              value="5500"
              description="<span
                class='text-sm font-weight-bolder text-success'
                >+550</span> since yesterday"
              :icon="{
                component: 'ni ni-bell-55',
                background: 'bg-gradient-info',
                shape: 'rounded-circle',
              }"
            />
          </div>

          <div class="col-lg-3 col-md-6 col-12">
            <mini-statistics-card
              title="Epic AC Coverage"
              value="62%"
              description="of <span
                class='text-sm font-weight-bolder text-primary'
                >19</span> total ACs"
              :icon="{
                component: 'ni ni-paper-diploma',
                background: 'bg-gradient-success',
                shape: 'rounded-circle',
              }"
            />
          </div>
          <div class="col-lg-3 col-md-6 col-12">
            <mini-statistics-card
              title="Average ETA(ms)"
              value="2000"
              description="<span>&nbsp;</span>"
              :icon="{
                component: 'ni ni-sound-wave',
                background: 'bg-gradient-warning',
                shape: 'rounded-circle',
              }"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="card col-md-12 mt-4">
        <h4 class="card-title mt-4">Send Event(s) or AC(s)</h4>
        <form>
          <div class="row">
            <div class="col-md-6">
              <div class="form-group">
                <label for="sel1">Select AC(s):</label>
                <select multiple="true" class="form-control" v-model="selectedACs" @change="selectACs($event)" >
                  <option v-for="ac in acList" :key="ac.id" :value="ac.id">{{ac.name}}</option>
                </select>
              </div>            
            </div>
            <div class="col-md-6">
              <div class="form-group">
                <label for="sel1">Select Event(s):</label>
                <select multiple="true" class="form-control" v-model="selectedEvents" @change="selectEvents($event)" >
                  <option v-for="event in eventsList" :key="event.id" :value="event.id">{{event.name}}</option>
                </select>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-md-12">
              <div class="form-group">
                <label>Event JSON</label>
                <textarea rows="10" class="form-control border-input"
                          placeholder=""
                          v-model="formattedJson"
                          >
                  </textarea>
              </div>
            </div>
          </div>
          <div class="text-center">
            <button type="submit" class="btn btn-info btn-fill float-right">
              Publish
            </button>
            <button type="submit" @click="handleClear" class="btn btn-secondary btn-fill float-right clear-btn">
              Clear
            </button>
          </div>
          <div class="clearfix"></div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>


  export default {
    components: {

    },
    data () {
      return {
        selectedEvents: [{id: 0, name: "Select Event"}],
        eventsList: [],
        selectedACs: [],
        acList: [],
        jsonEvents: [],
      }
    },
    mounted () {
      const assetsContext = require.context('@/assets/eventsjson', false, /\.(json)$/);
      const jsonFiles = assetsContext.keys().map(key => assetsContext(key));
      console.log(jsonFiles);
 
      // Build the event select options.
      for(let i = 0; i < jsonFiles.length; i++) {
        const jsonArray = jsonFiles[i]
        for(let j = 0; j < jsonArray.length; j++) {
          // If associated with an AC
          if( jsonArray[j].acID ) {
            this.acList.push(jsonArray[j])
          }
          // Else, just a list of events
          else {
            this.eventsList.push(jsonArray[j])
          }
        }
      }
    },
    methods: {
      // Build events selects & table CRUD list
      selectEvents() {
        this.selectedACs = [];
        if( this.selectedEvents.length > 0 ) {
          this.jsonEvents = [];
        
          for( let i = 0; i < this.selectedEvents.length; i++ ) {
            const event = this.eventsList.find(obj => obj.id === this.selectedEvents[i]);
            this.jsonEvents.push(event)

            //this.tableData.push(event)
          }
        }
      },
      selectACs() {
        this.selectedEvents = [];
        if( this.selectedACs.length > 0 ) {
          this.jsonEvents = [];
        
          for( let i = 0; i < this.selectedACs.length; i++ ) {
            const event = this.acList.find(obj => obj.id === this.selectedACs[i]);
            this.jsonEvents.push(event)
          }
        }
      },
      handleClear() {
        this.selectedACs = [];
        this.selectedEvents = [];
        this.jsonEvents = [];
      },
    },
    computed: {
      formattedJson() {
        return this.jsonEvents.length > 0 ? JSON.stringify(this.jsonEvents, null, 2) : '';
      }
    }
 
  }
</script>
<style>
  .center {
    margin: auto;
  }
  .clear-btn {
    margin-left: 10px;
  }
  .cardheader {
    width: 25%;
  }
  .cardbtn {
    margin-top: 15px;
    margin-right: 15px;
    position:absolute;
    top:0;
    right:0;
  }
 
</style>
