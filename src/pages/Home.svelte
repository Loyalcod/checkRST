<script>
    import Footer from "../components/Footer.svelte";
    import FormModel from "../components/FormModel.svelte";
    import Headers from "../components/Headers.svelte";
    import ShowModel from "../components/ShowModel.svelte";


    let src = './images/result1.jpeg'

    let showInModel = false;

    const toggolModel = ()=>{
        showInModel = !showInModel
    }

    let email;
    let regNo;

    const prepareResult = (e) =>{
        email = e.detail.email
        regNo = e.detail.regNo
        if((email == '' || email == undefined) || (regNo == '' || regNo == undefined)){
            alert("please fill in the mixing space before submiting")
        }else{
            window.location.assign(window.location.href + `result/${email}/${regNo}`)
        }
    }



</script>

<Headers on:click={toggolModel} />



<ShowModel {showInModel} on:click={toggolModel} >
	<FormModel on:studentDetail={prepareResult} />
</ShowModel>

<img src={src} alt="">

<Footer/>

<style>
	img{
		width: 100vw;
		height: 75vh;
		object-fit: cover;
		display: block;
	}
</style>
