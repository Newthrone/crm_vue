<template>
  <ul class="sidenav app-sidenav" :class="{open: value}">
    <router-link tag="li"
                 active-class="active"
                 :to="link.url"
                 :exact="link.exact"
                 v-for="(link, index) of links" :key="index">
      <a class="waves-effect waves-orange pointer">
        {{ link.title }}
      </a>
    </router-link>
  </ul>
</template>

<script>
export default {
  name: "Sidebar",
  data: () => ({
    links: [
      {title: 'Счёт', url: '/', exact: true},
      {title: 'История', url: '/history'},
      {title: 'Планирование', url: '/planning'},
      {title: 'Новая запись', url: '/record'},
      {title: 'Категории', url: '/categories'},
    ]
  }),
  props: ['value']
};
</script>

<style>
</style>
