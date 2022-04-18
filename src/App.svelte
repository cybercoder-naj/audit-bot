<script>
  import Navbar from './components/Navbar.svelte'

  import Home from './pages/Home.svelte'
  import Bot from './pages/Bot.svelte'

  import Router from 'svelte-spa-router'

  const routes = {
    '/': Home,
    '/bot': Bot
  }
</script>

<header>
  <Navbar />
</header>
<main>
  <Router {routes} />
</main>
