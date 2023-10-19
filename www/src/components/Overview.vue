<template>
  <div>

    <h4>Metadata</h4>
    <b-table stacked :items="items"></b-table>

    <div v-for="item in items" :key="item">
      <b-row class="mb-2">
        <b-col> {{ item }} 
          <div v-if="item.duration > 100">RED</div>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Overview',
  props: ['info'],
  data() {
    return {
      stream_fields: [
        'id',
        'start_time',
        'duration',
        'codec_type',
        'codec_name',
        'format',
        'bit_rate',
        'profile',
        'level',
        'width',
        'height',
        'channels',
        'sample_rate',
        'frame_size',
        { key: 'show_details', label: 'Tags' },
      ],
      chapter_fields: ['id', 'time_base', 'start', 'end', { key: 'show_details', label: 'Tags' }],
    }
  },
  computed: {
    items() {
      return [
        {
          name: this.info.name,
          duration: this.info.duration,
          bit_rate: this.info.bit_rate,
        },
      ]
    },
    versions() {
      return [
        {
          libavutil:  this.info.versions.libavutil,
          libavcodec:  this.info.versions.libavcodec,
          libavformat:  this.info.versions.libavformat,
        },
      ]
    },
  },
}
</script>
