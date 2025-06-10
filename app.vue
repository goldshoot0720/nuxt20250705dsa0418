<template>
  <div>
    <nav style="margin-bottom: 1rem">
      <NuxtLink to="/">Home</NuxtLink> |
      <NuxtLink to="/Stack">Stack</NuxtLink> |
      <NuxtLink to="/Queue">Queue</NuxtLink> |
      <NuxtLink to="/Tree">Tree</NuxtLink>
    </nav>
    <nav style="margin-bottom: 1rem">
      <NuxtLink to="/Date">Date</NuxtLink> |
      <NuxtLink to="/Vue3">Vue3</NuxtLink> | <NuxtLink to="/">保留2</NuxtLink> |
      <NuxtLink to="/">保留3</NuxtLink>
    </nav>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>
