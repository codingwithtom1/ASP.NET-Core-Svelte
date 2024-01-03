<script lang='ts'>
    import svelteLogo from '../assets/svelte.svg'
    import Counter from '../components/Counter.svelte'
    import WeatherForecast from '../components/WeatherForecast.svelte';
    import { Link } from 'svelte-routing';
    import AuthorizeView from '../AuthorizeView.svelte';
    import Logout from '../components/Logout.svelte';
    
    </script>
    
    <AuthorizeView let:user_identity_email>
    <main>
        <div>
          <a href="https://svelte.dev" target="_blank" rel="noreferrer">
            <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
          </a>
        </div>
        <h1>Svelte Demo</h1>
        <Logout>Log Out {user_identity_email}</Logout> |
        <Link to="/register">Register</Link>
        <div class="card">
          <Counter />
          <WeatherForecast/>
        </div>
      </main>
      
      <style>
        .logo {
          height: 6em;
          padding: 1.5em;
          will-change: filter;
          transition: filter 300ms;
        }
        .logo:hover {
          filter: drop-shadow(0 0 2em #646cffaa);
        }
        .logo.svelte:hover {
          filter: drop-shadow(0 0 2em #ff3e00aa);
        }
        
      </style>
    </AuthorizeView>