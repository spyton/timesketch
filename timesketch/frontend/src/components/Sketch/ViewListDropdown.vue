<!--
Copyright 2019 Google Inc. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->
<template>
  <div class="dropdown" v-bind:class="{'is-active': viewListDropdownActive}">
    <div class="dropdown-trigger">
      <a class="button" v-bind:class="{'is-rounded': isRounded}" aria-haspopup="true" aria-controls="dropdown-menu" v-on:click="viewListDropdownActive = !viewListDropdownActive">
        <span>{{ title || 'Views' }}</span>
        <span class="icon is-small">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </a>
    </div>
    <div class="dropdown-menu" id="dropdown-menu" role="menu">
      <div class="dropdown-content">
        <span class="dropdown-item" v-if="meta.views && meta.views.length < 1">No saved views</span>
        <a class="dropdown-item" v-on:click="setActiveView(view)" v-for="view in meta.views" :key="view.id">
          <span>{{ view.name }}</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['isRounded', 'title'],
  data () {
    return {
      viewListDropdownActive: false
    }
  },
  methods: {
    setActiveView: function (view) {
      this.$emit('setActiveView', view)
      this.viewListDropdownActive = false
    }
  },
  computed: {
    meta () {
      return this.$store.state.meta
    }
  }
}
</script>

<!-- CSS scoped to this component only -->
<style scoped lang="scss"></style>
