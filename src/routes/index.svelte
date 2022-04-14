<svelte:head>
    <title>Bank Search</title>
</svelte:head>

<h1>Bank Search</h1>
<div class="row">
    <div class="col">
        <input class="form-control"
               placeholder="Institution"
               type="text" name="search" bind:value={institution} on:keypress={search}>
    </div>
    <div class="col">
        <input class="form-control"
               placeholder="State"
               type="text" name="search" bind:value={usState} on:keypress={search}>
    </div>
</div>

{#if showSearching}
    <p>Searching for {institution}...</p>
{/if}

{#if showResults}
<!--    The data is not empty {returnData.data.data}-->
<h3>count: {returnData.data.totals.count}</h3>
<table class="table table-striped">
    <thead>
    <tr>
        <th>Cert</th>
        <th>Name</th>
        <th>City</th>
        <th>State</th>
        <th>Zip</th>
    </tr>
    </thead>
    <tbody>
    {#each returnData.data.data as d}
    <tr>
        <td><a href="/cert/{d.data.CERT}" class="btn btn-primary">{d.data.CERT}</a></td>
        <td>{d.data.NAME}</td>
        <td>{d.data.CITY}</td>
        <td>{d.data.STNAME}</td>
        <td>{d.data.ZIP}</td>
    </tr>
    {/each}
    </tbody>
</table>
{/if}

<script>
    import axios from 'axios'

    let showSearching,showResults = false
    let institution, usState = "";
    let returnData = {};

    async function search(e) {
        if (e.code !== "Enter") {
            return;
        }
        showSearching = true;

        let myHeaders = new Headers();
        myHeaders.append("Accept", "application/json");

        const query = `
        https://banks.data.fdic.gov/api/institutions?filters=ACTIVE:1 AND STNAME:\\"${usState}\\"&limit=10000&search=NAME:${institution}&fields=CITY,STNAME,NAME,ZIP,CERT&format=json&sort=NAME,STNAME,CITY,CERT
        `;

        try {
            const instance = axios.create({'headers': {'Accept': 'application/json'}});
            const response = await instance.get(query);
            returnData = response;
            showResults = true;
            showSearching = false;
            console.log(response);
        } catch (error) {
            console.error(error);
        }
    }
</script>

<style>

</style>