<h1>Reports for Cert: {cert}</h1>
<hr>
{#await financials}
    <p>...loading</p>
{:then res}
    <div class="row mb-5">
        <div class="col-md-6">
            <label for="report_date" class="form-label">Select Report Date</label>
            <select name="report_date" id="report_date" class="form-select" bind:value={selectedIndex}>
                {#each res.data as d, k}
                    <option value="{k}">{FormatDate(d.data.REPDTE)}</option>
                {/each}
            </select>
        </div>
    </div>
{/await}

{#if selected != null }
    <div class="row">
        <div class="col-md-6">
            <h2>Raw Data</h2>
            <table class="table table-striped table-sm">
                <tbody>
                <tr>
                    <th>ID</th>
                    <td>{selected.ID}</td>
                </tr>
                <tr>
                    <th>REPDTE</th>
                    <td>{FormatDate(selected.REPDTE)}</td>
                </tr>
                <tr>
                    <th>REPYEAR</th>
                    <td>{selected.REPYEAR}</td>
                </tr>
                <tr>
                    <th>NAME</th>
                    <td>{selected.NAME}</td>
                </tr>
                <tr>
                    <th>CITY</th>
                    <td>{selected.CITY}</td>
                </tr>
                <tr>
                    <th>FLDOFF</th>
                    <td>{selected.FLDOFF}</td>
                </tr>
                <tr>
                    <th>ZIP</th>
                    <td>{selected.ZIP}</td>
                </tr>
                <tr>
                    <th>STNAME</th>
                    <td>{selected.STNAME}</td>
                </tr>
                <tr>
                    <th>ACTIVE</th>
                    <td>{selected.ACTIVE}</td>
                </tr>
                <tr>
                    <th>CERT</th>
                    <td>{selected.CERT}</td>
                </tr>
                <tr>
                    <th>ASSET</th>
                    <td>{FormatCash(selected.ASSET)} M</td>
                </tr>
                <tr>
                    <th>CHBAL</th>
                    <td>{FormatCash(selected.CHBAL)} M</td>
                </tr>
                <tr>
                    <th>CHBALNI</th>
                    <td>{selected.CHBALNI}</td>
                </tr>
                <tr>
                    <th>CHFRB</th>
                    <td>{selected.CHFRB}</td>
                </tr>
                <tr>
                    <th>DEP</th>
                    <td>{selected.DEP}</td>
                </tr>
                <tr>
                    <th>EQ</th>
                    <td>{selected.EQ}</td>
                </tr>
                <tr>
                    <th>FREPO</th>
                    <td>{selected.FREPO}</td>
                </tr>
                <tr>
                    <th>ICHBAL</th>
                    <td>{selected.ICHBAL}</td>
                </tr>
                <tr>
                    <th>ICHBALQ</th>
                    <td>{selected.ICHBALQ}</td>
                </tr>
                <tr>
                    <th>IFREPO</th>
                    <td>{selected.IFREPO}</td>
                </tr>
                <tr>
                    <th>IFREPOQ</th>
                    <td>{selected.IFREPOQ}</td>
                </tr>
                <tr>
                    <th>ILNDOM</th>
                    <td>{selected.ILNDOM}</td>
                </tr>
                <tr>
                    <th>ILNDOMQ</th>
                    <td>{selected.ILNDOMQ}</td>
                </tr>
                <tr>
                    <th>ILS</th>
                    <td>{selected.ILS}</td>
                </tr>
                <tr>
                    <th>ILSQ</th>
                    <td>{selected.ILSQ}</td>
                </tr>
                <tr>
                    <th>ISC</th>
                    <td>{selected.ISC}</td>
                </tr>
                <tr>
                    <th>ISCQ</th>
                    <td>{selected.ISCQ}</td>
                </tr>
                <tr>
                    <th>LNCI</th>
                    <td>{selected.LNCI}</td>
                </tr>
                <tr>
                    <th>LNLSGR</th>
                    <td>{selected.LNLSGR}</td>
                </tr>
                <tr>
                    <th>LNLSNET</th>
                    <td>{selected.LNLSNET}</td>
                </tr>
                <tr>
                    <th>NETINC</th>
                    <td>{selected.NETINC}</td>
                </tr>
                <tr>
                    <th>NETINCQ</th>
                    <td>{selected.NETINCQ}</td>
                </tr>
                <tr>
                    <th>SC</th>
                    <td>{selected.SC}</td>
                </tr>
                </tbody>
            </table>
        </div>
    </div>
{/if}

<script context="module">
    export function load({params}) {
        return {
            props: {
                cert: params.cert
            }
        }
    }
</script>

<script>
    export let cert
    import axios from 'axios'

    let selectedIndex = 0;
    $: selected = data ? data.data[selectedIndex].data : null;
    let data = null;
    let financials = GetFinancials();

    function FormatDate(date) {
        return date.slice(4, 6) + "/" +
            date.slice(6, 8) + "/" +
            date.slice(0, 4);
    }

    function FormatCash(cash) {
        let number = new Intl.NumberFormat().format(cash);
        return "$" + number;
    }

    async function GetFinancials() {
        let response = await axios.get("https://banks.data.fdic.gov/api/financials", {
            params: {
                fields: "ID,NAME,CITY,FLDOFF,ZIP,STNAME,ACTIVE,CERT,ASSET,CHBAL,CHBALNI,CHFRB," +
                    "DEP,EQ,FREPO,ICHBAL,ICHBALQ,IFREPO,IFREPOQ,ILNDOM,ILNDOMQ,ILS,ILSQ,ISC,ISCQ," +
                    "LNCI,LNLSGR,LNLSNET,NETINC,NETINCQ,SC,REPDTE,REPYEAR",
                filters: "CERT:" + cert + " AND ACTIVE:1",
                format: "json",
                limit: "12",
                sort_by: "REPDTE",
                sort_order: "DESC",
            },
            headers: {
                "Accept": "application/json"
            }
        })

        if (response.status < 300) {
            selected = response.data.data[selectedIndex].data
            data = response.data;
            return response.data;
        } else {
            throw new Error("Could not retrieve the data.");
        }
    }

</script>