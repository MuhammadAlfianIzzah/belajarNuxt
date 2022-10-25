<template>
  <div>
    <v-btn @click="toggle">
      Show {{ seen }}
    </v-btn>
    <p v-if="seen">Now you see me</p>
    <a :[href]="url">aaa</a>
    <button name="button" @click="greet">Greet</button>

    <!-- <a :[href]="url">Link</a> -->

  </div>

</template>

<script>
export default {
  name: "IndexPage",

  methods: {
    toggle() {
      this.seen = !this.seen
    }, greet(event) {
      // `this` inside methods points to the current active instance
      alert(`Hello ${this.name}!`)
      // `event` is the native DOM event
      if (event) {
        alert(event.target.tagName)
      }
    }
  },
  data() {
    return {
      href: "href",
      eventName: "dragenter",
      url: "www.google.com",
      seen: false,
      rawHtml: "hello world"
    }
  }
}
</script>
