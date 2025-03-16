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
  </div>
</template>
