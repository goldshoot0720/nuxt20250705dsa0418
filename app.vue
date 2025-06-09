<template>
  <div>
    <nav style="margin-bottom: 1rem">
      <NuxtLink to="/">Home</NuxtLink> |
      <NuxtLink to="/Stack">Stack</NuxtLink> |
      <NuxtLink to="/Queue"> Queue</NuxtLink>
    </nav>
    <nav style="margin-bottom: 1rem">
      <NuxtLink to="/Date">Date</NuxtLink> | <NuxtLink to="/">保留1</NuxtLink> |
      <NuxtLink to="/">保留2</NuxtLink> | <NuxtLink to="/">保留3</NuxtLink>
    </nav>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>
