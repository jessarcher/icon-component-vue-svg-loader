<template>
  <component :is="iconComponent" class="inline-block fill-current" style="height: 1em; width: 1em; vertical-align: -0.125em" />
</template>

<script>

// const icons = {
//   'home': require('../assets/icons/icon-home.svg').default,
//   'user': require('../assets/icons/icon-user.svg').default,
//   'key': require('../assets/icons/icon-key.svg').default,
// }

const icons = {}

const requireComponents = require.context('../assets/icons/', false, /.svg$/)

requireComponents.keys().forEach(fileName => {
  const iconName = fileName.replace(/^\.\/icon-(.+)\.svg$/, '$1')
  const componentConfig = requireComponents(fileName)
  icons[iconName] = componentConfig.default || componentConfig
})

export default {
  props: {
    name: {
      type: String,
      required: true,
      validator(value) {
        return Object.prototype.hasOwnProperty.call(icons, value)
      }
    }
  },

  computed: {
    iconComponent() {
      return icons[this.name]
    },
  }
}
</script>>
