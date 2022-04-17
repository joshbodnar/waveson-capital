<svelte:head>
    <title>Bank Search</title>
</svelte:head>

<h1>Bank Search</h1>
<div class="row">
    <div class="col">
        <label for="institution" class="form-label">Institution Name</label>
        <input class="form-control"
               placeholder="Institution"
               type="text" name="institution" id="institution"
               bind:value={institution} on:keypress={search}>
    </div>
    <div class="col">
        <label for="state" class="form-label">State</label>
        <input class="form-control"
               placeholder="State"
               type="text" name="state" id="state"
               bind:value={usState} on:keypress={search}>
    </div>
</div>
<hr>

{#if showSearching}
    <p>Searching for {institution}...</p>
{/if}

{#if showResults}
    <h3>
        <small>
            count: {returnData.data.totals.count}
        </small>
    </h3>
    <table class="table table-sm table-striped">
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
                <td><a href="/cert/{d.data.CERT}" class="btn btn-sm btn-primary d-block">{d.data.CERT}</a></td>
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

    let showSearching, showResults = false
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