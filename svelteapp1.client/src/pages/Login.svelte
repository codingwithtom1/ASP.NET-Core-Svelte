<script lang="ts">
    import { navigate } from "svelte-routing";
    let email = "";
    let password = "";
    let message = "";
    let rememberme = false;

    function handleRegister() {
        navigate("/register");
    }

    async function submitForm() {
        const data = { email, password };
        let url = "/login";
        if (rememberme) url += "?useCookies=true";
        else url += "?useSessionCookies=true";

        const response = await fetch(url, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(data),
        });
        const result = await response;
        if (response.ok) window.location.href = "/";
        else message = "Error Logging in.";
    }
</script>

<div class="box">
    <form on:submit|preventDefault={submitForm}>
        <div class="table">
            <div class="row">
                <div class="col">Email:</div>
                <div class="col">
                    <input
                        type="email"
                        placeholder="Enter your email"
                        bind:value={email}
                    />
                </div>
            </div>
            <div class="row">
                <div class="col">Password:</div>
                <div class="col">
                    <input
                        type="password"
                        placeholder="Enter your password"
                        bind:value={password}
                    />
                </div>
            </div>
        </div>
        <div>
            <input id="checkbox" type="checkbox" bind:checked={rememberme} />
            Remember Me
        </div>

        <button type="submit">Login</button>
        <p>{message}</p>
    </form>
    <button on:click={handleRegister}>Register</button>
</div>
