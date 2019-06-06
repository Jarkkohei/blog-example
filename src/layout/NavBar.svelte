<script>
    import { Link } from 'svelte-routing';
    import NavLink from '../components/NavLink.svelte';
</script>

<nav>
  <div class="nav-wrapper">
    <div class="container">
      <Link to="/"><span class="brand-logo">Blog-example</span></Link>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <li class="link-wrapper"><NavLink to="/">Home</NavLink></li>
        <li class="link-wrapper"><NavLink to="/about">About</NavLink></li>
      </ul>
    </div>
  </div>
</nav>
