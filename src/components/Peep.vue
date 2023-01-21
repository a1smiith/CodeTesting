<template>
  <svg style="background-color: rgba(194, 191, 190, 0.3);"
    width="100%"
    height="100%"
    viewBox="0 0 1200 1200"
    xmlns="http://www.w3.org/2000/svg"
    preserveAspectRatio="xMidYMid meet"
    fill="none"
  >
    <path
      v-if="transparent"
      d="M0 0H1366V1533H-1366V0Z"
      :fill="background"
    />
    <component
      :is="body"
      :skin-color="skinColor"
      :body-color="bodyColor"
    />
    <component
      :is="head"
      :skin-color="skinColor"
      :hair-color="hairColor"
    />
    <component :is="face" />
    <component :is="facialHair" />
    <component :is="accessories" />
  </svg>
</template>
<script>
export default {
  name: 'Peep',
  props: {
    head: {
      type: String,
      default () {
        return 'HeadBunv2'
      }
    },
    skinColor: {
      type: String,
      default () {
        return 'white'
      }
    },
    hairColor: {
      type: String,
      default () {
        return 'black'
      }
    },
    body: {
      type: String,
      default () {
        return 'BodyWhatever'
      }
    },
    transparent: {
      type: Boolean,
      default: false
    },
    background: {
      type: String,
      default () {
        return '#ffffff'
      }
    },
    face: {
      type: String,
      default () {
        return 'FaceSmile'
      }
    },
    accessories: {
      type: String,
      default: null
    },
    facialHair: {
      type: String,
      default: null
    }
  }
}
</script>
