<script lang="ts">
    import { navigate } from "svelte-routing";

    let email: string = "";
    let password: string = "";
    let confirm: string = "";
    let message: string = "";
    let valid: boolean = false;

    // A simple function to check if an email is valid

    function handleLogin() {
        navigate("/login");
    }

    function validateEmail(email: string) {
        const regex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
        return regex.test(email);
    }

    // A function to check if the form inputs are valid and set the message accordingly
    function validateForm() {
        if (!email || !password || !confirm) {
            message = "Please fill in all the fields.";
            valid = false;
        } else if (!validateEmail(email)) {
            message = "Please enter a valid email address.";
            valid = false;
        } else if (password !== confirm) {
            message = "The passwords do not match.";
            valid = false;
        } else {
            message = "The form is valid.";
            valid = true;
        }
    }

    // A function to submit the form data to the /register api as a json object
    async function submitForm() {
        validateForm();
        if (valid) {
            const data = { email, password };
            const response = await fetch("/register", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(data),
            });
            const result = await response;
            if (response.ok) message = "Success.";
            else message = "Error registering.";
        }
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
                    on:input={validateForm}
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
                    on:input={validateForm}
                />
            </div>
        </div>
        <div class="row">
            <div class="col">Password: (confirm)</div>
            <div class="col">
                <input
                    type="password"
                    placeholder="Confirm your password"
                    bind:value={confirm}
                    on:input={validateForm}
                />
            </div>
        </div>
    </div>
    <button type="submit">Register</button>

    <p>{message}</p>
</form>
<button on:click={handleLogin}>Go to Login</button>
</div>