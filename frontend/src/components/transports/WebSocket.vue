<template>
  <v-row>
    <v-col cols="12" sm="6" md="4">
      <v-text-field
      :label="$t('transport.path')"
      hide-details
      v-model="transport.path">
      </v-text-field>
    </v-col>
    <v-col cols="12" sm="6" md="4">
      <v-text-field
      label="Max Early Data"
      hide-details
      type="number"
      min="0"
      v-model.number="max_early_data">
      </v-text-field>
    </v-col>
    <v-col cols="12" sm="6" md="4">
      <v-text-field
      label="Early Data Header Name"
      hide-details
      v-model="transport.early_data_header_name">
      </v-text-field>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { WebSocket } from '../../types/transport'
export default {
  props: ['transport'],
  data() {
    return {
    }
  },
  computed: {
    WS(): WebSocket {
      return <WebSocket> this.$props.transport
    },
    max_early_data: {
      get() { return this.WS.max_early_data ? this.WS.max_early_data : '' },
      set(newValue:number) { this.$props.transport.max_early_data = newValue != 0 ? newValue : undefined }
    },
  },
  mounted() {
    this.WS.early_data_header_name = 'Sec-WebSocket-Protocol'
    this.WS.path = '/'
  }
}
</script>