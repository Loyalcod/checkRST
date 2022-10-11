<script>
    import { createEventDispatcher } from "svelte";
   

    let dispatcher = createEventDispatcher()

    let email;
    let regNo;
    let formInput;

    let takeInputs = () =>{
        formInput = {email,regNo}
               
        dispatcher('studentDetail', formInput)
    }

    

    

</script>

<form on:submit|preventDefault={takeInputs}>
    <h1 class="h4 text-center fs-4">Check Your Result</h1>

    <div class="form-group py-2">
        <label for="">Email Address </label>
        <input type="text" class="form-control" bind:value={email}  placeholder="enter your email">
    </div>

    <div class="form-group py-2">
        <label for="">Registration No. </label>
        <input type="number" class="form-control" bind:value={regNo} placeholder="enter your email">
    </div>
    
    <hr>

    <button class="btn bg-primary text-white">Submit</button>
</form>