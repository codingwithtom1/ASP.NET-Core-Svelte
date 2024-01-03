<script lang='ts'>
    import Login from './pages/Login.svelte';

    let user_identity_email : string = '';
   
    async function IsAuthenticated() {
        const response = await fetch("/pingauth");
        let status : number  = response.status;
        
       
        let authenticated : boolean = false;
        if (status != 200) {
            authenticated = false;    
            
        }
        else {  
            let j = await response.json();
            user_identity_email = j.email;
            authenticated = true;
        }
        return authenticated;
    }
    
</script>


{#await IsAuthenticated()}
<span>Checking Authentication</span>
{:then authenticated}
  {#if (authenticated) }
  <slot {user_identity_email}></slot>
  {:else}
    <Login/>
  {/if}
{/await}