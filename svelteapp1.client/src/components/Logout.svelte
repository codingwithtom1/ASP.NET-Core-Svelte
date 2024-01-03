<script lang='ts'>
    
    async function logout() {
      const response = await fetch('/logout', { method: 'POST' });
      if (response.ok) {
        window.location.href = '/';
      }
    }
  </script>
  
  <a href="/" on:click|preventDefault={logout}>
<slot></slot>
</a>
