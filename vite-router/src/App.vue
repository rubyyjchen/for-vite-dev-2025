
<template>
  <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/review">Review</RouterLink>
        <RouterLink to="/async">Async</RouterLink>
        <RouterLink to="/todo">Todo</RouterLink>
      </nav>
  </header>

  <RouterView />
</template>
