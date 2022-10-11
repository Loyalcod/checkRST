<script>
    import { onMount } from 'svelte';

    import Headers from "../components/Headers.svelte";
    import Footer from "../components/Footer.svelte";
    import Subjects from '../components/Subjects.svelte';
    import ShowModel from '../components/ShowModel.svelte';
    import FormModel from '../components/FormModel.svelte';
    
    let showInModel = false;

    const toggolModel = () => {
        showInModel = !showInModel
    }


    export let urlParam
    let email = urlParam.email;
    let regNo = urlParam.regNo
    let result = []

    let total = 0;
    let subScore = 0;
    let percentage = 0;

    onMount(async () =>{
        try {
            const response = await fetch(`http://localhost:2000/result/${email}/${regNo}`)
            const data = await response.json()
            // console.log(data)
            result = data
            console.log(result)

            if(result[0].resultId.length !== 0){
                result[0].resultId.forEach(singleResult =>{
                    total += 100;
                    subScore += singleResult.mark;

                });

                percentage = (subScore/total * 100)
            }

        } catch (error) {
            console.log(error)
        }
    })

   

    const prepareResult = (e) => {
        let email = e.detail.email
        let regNo = e.detail.regNo
        console.log(e.detail)

        if((email == '' || email == undefined) || (regNo == '' || regNo == undefined)){
            alert("please fill in the mixing space before submiting")
        }else{
            let url = new URL(window.location.href + `result/${email}/${regNo}`)
            let origin = url.origin
            window.location.assign(origin+`/result/${email}/${regNo}`)
        }
    }

    

</script>

<Headers on:click={toggolModel} />

<ShowModel {showInModel} on:click={toggolModel}>
    <FormModel on:studentDetail= {prepareResult} />
</ShowModel>



{#if result.length !== 0}
{#if result !== `result don't exist`}
<div class="container">
    <h4 class="py-4 mt-2 text-center">Result Details</h4>
    <div class="nameCon">
        <p class="m-1"><strong>Name:</strong> <span>{result[0].studentName}</span></p>
        <p class="m-1"><strong>Registration No.:</strong> <span>Mouau/cmp/{result[0].regNo}</span></p>
        {#if result[0].resultId.length !== 0}
        <p class="m-1"><strong>Grade:</strong> <span>{result[0].studentClass.className}</span></p>
        {:else}
        <p class="m-1"><strong>Grade:</strong> <span>pending</span></p>
       {/if}
    </div>
    <table class="table table-bordered table striped shadow-lg rounded mt-3">
        <thead>
            <tr>
                <th>S/N</th>
                <th>Subject</th>
                <th>Mark</th>
            </tr>
        </thead>
        <tbody class="table-group-divider">

            {#each result[0].resultId as singleResult, i}
                <Subjects {singleResult} {i}/>
            {/each}
           
            <tr>
                <td colspan="2" class="text-center"><strong>Total</strong></td>
                <td>{subScore} <strong>Out of</strong> {total}</td>
            </tr>
            <tr>
                <td colspan="2" class="text-center"><strong>Percentage</strong></td>
                <td> <strong>{percentage}</strong> </td>
            </tr>
        </tbody>
    </table>

    <button class="btn btn-primary btn-white px-5" on:click= { () => {window.print()}}>print</button>
    <hr>

    <a href="/" class="text-decoration-none text-dark">Back Home</a>
</div>
{:else}
<h4 class="py-5 text-center">No such Student </h4>
{/if}
{/if}
<Footer/>

