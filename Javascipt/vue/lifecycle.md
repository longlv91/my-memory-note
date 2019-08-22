# Vue lifecycle Hooks

Ref:
1. [Understanding Vue.js Lifecycle Hooks](https://alligator.io/vuejs/component-lifecycle/)
2. [VueJS Home page](https://vuejs.org/v2/guide/instance.html)


## Lifecycle Diagram

<p align="center"><img src="./images/lifecycle.png" width="450"></p>


### Creation (Initialization)

Creation hooks are the very first hooks that run in your component. They allow you to perform actions before your component has even been added to the DOM. Unlike any of the other hooks, creation hooks are also run during server-side rendering.

Use creation hooks if you need to set things up in your component both during client rendering and server rendering. You will not have access to the DOM or the target mounting element (this.$el) inside of creation hooks.

#### beforeCreate

The beforeCreate hook runs at the very initialization of your component. data has not been made reactive, and events have not been set up yet.

```
<script>
export default class ExamleComponent extends Vue {
  beforeCreate() {
    console.log('Nothing gets called before me!')
  }
}
</script>
```

#### created

In the created hook, you will be able to access reactive data and events are active. Templates and Virtual DOM have not yet been mounted or rendered.

```
<script>
export default class ExamleComponent extends Vue {
  created() {
    this.property = 'Example property update.'
    console.log('propertyComputed will update, as this.property is now reactive.')
  }
}
</script>
```

### Mounting (DOM Insertion)

Mounting hooks are often the most-used hooks, for better or worse. They allow you to access your component immediately before and after the first render. They do not, however, run during server-side rendering.

Use if: You need to access or modify the DOM of your component immediately before or after the initial render.

Do not use if: You need to fetch some data for your component on initialization. Use created (or created + activated for keep-alive components) for this instead, especially if you need that data during server-side rendering.

#### beforeMount

The beforeMount hook runs right before the initial render happens and after the template or render functions have been compiled. Most likely you’ll never need to use this hook. Remember, it doesn’t get called when doing server-side rendering.

```
<script>
export default class ExamleComponent extends Vue {
  beforeMount() {
    console.log(`this.$el doesn't exist yet, but it will soon!`)
  }
}
</script>
```

#### mounted

In the mounted hook, you will have full access to the reactive component, templates, and rendered DOM (via. this.$el). Mounted is the most-often used lifecycle hook. The most frequently used patterns are fetching data for your component (use created for this instead,) and modifying the DOM, often to integrate non-Vue libraries.

```
<template>
  <p>I'm text inside the component.</p>
</template>

<script>
export default class ExamleComponent extends Vue {
  mounted() {
    console.log(this.$el.textContent) // I'm text inside the component.
  }
}
</script>
```

### Updating (Diff & Re-render)

Updating hooks are called whenever a reactive property used by your component changes, or something else causes it to re-render. They allow you to hook into the watch-compute-render cycle for your component.

Use if: You need to know when your component re-renders, perhaps for debugging or profiling.

Do not use if: You need to know when a reactive property on your component changes. Use computed properties or watchers for that instead.

#### beforeUpdate

The beforeUpdate hook runs after data changes on your component and the update cycle begins, right before the DOM is patched and re-rendered. It allows you to get the new state of any reactive data on your component before it actually gets rendered.

```
<script>
export default class ExamleComponent extends Vue {
  beforeUpdate() {
    console.log(this.counter) // Logs the counter value every second, before the DOM updates.
  },

  created() {
    setInterval(() => {
      this.counter++
    }, 1000)
  }
}
</script>
```

#### updated

The updated hook runs after data changes on your component and the DOM re-renders. If you need to access the DOM after a property change, here is probably the safest place to do it.

```
<template>
  <p ref="dom-element">{{counter}}</p>
</template>
<script>
export default class ExamleComponent extends Vue {
  data() {
    return {
      counter: 0
    }
  },

  updated() {
    // Fired every second, should always be true
    console.log(+this.$refs['dom-element'].textContent === this.counter)
  },

  created() {
    setInterval(() => {
      this.counter++
    }, 1000)
  }
}
</script>
```

### Destruction (Teardown)

Destruction hooks allow you to perform actions when your component is destroyed, such as cleanup or analytics sending. They fire when your component is being torn down and removed from the DOM.

#### beforeDestroy

beforeDestroy is fired right before teardown. Your component will still be fully present and functional. If you need to cleanup events or reactive subscriptions, beforeDestroy would probably be the time to do it.

```
<script>
export default class ExamleComponent extends Vue {
  data() {
    return {
      someLeakyProperty: 'I leak memory if not cleaned up!'
    }
  },

  beforeDestroy() {
    // Perform the teardown procedure for someLeakyProperty.
    // (In this case, effectively nothing)
    this.someLeakyProperty = null
    delete this.someLeakyProperty
  }
}
</script>
```

#### destroyed

By the time you reach the destroyed hook, there’s pretty much nothing left on your component. Everything that was attached to it has been destroyed. You might use the destroyed hook to do any last-minute cleanup or inform a remote server that the component was destroyed like a sneaky snitch.

```
<script>
import MyCreepyAnalyticsService from './somewhere-bad'

export default class ExamleComponent extends Vue {
  destroyed() {
    console.log(this) // There's practically nothing here!
    MyCreepyAnalyticsService.informService('Component destroyed. All assets move in on target on my mark.')
  }
}
</script>
```

### Other Hooks

There are two other hooks, activated and deactivated. These are for keep-alive components, a topic that is outside the scope of this article. Suffice it to say that they allow you to detect when a component that is wrapped in a <keep-alive></keep-alive> tag is toggled on or off. You might use them to fetch data for your component or handle state changes, effectively behaving as created and beforeDestroy without the need to do a full component rebuild.