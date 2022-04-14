<h1>Searching Cert: {cert}</h1>

{#await financials}
    <p>...loading</p>
{:then res}
    <table class="table table-striped table-responsive">
        <thead>
        <tr>
<!--            <th>ID</th>-->
            <th>REPDTE</th>
<!--            <th>REPYEAR</th>-->
            <th>NAME</th>
            <th>CITY</th>
            <th>FLDOFF</th>
            <th>ZIP</th>
            <th>STNAME</th>
            <th>ACTIVE</th>
            <th>CERT</th>
            <th>ASSET</th>
            <th>CHBAL</th>
<!--            <th>CHBALNI</th>-->
<!--            <th>CHFRB</th>-->
<!--            <th>DEP</th>-->
<!--            <th>EQ</th>-->
<!--            <th>FREPO</th>-->
<!--            <th>ICHBAL</th>-->
<!--            <th>ICHBALQ</th>-->
<!--            <th>IFREPO</th>-->
<!--            <th>IFREPOQ</th>-->
<!--            <th>ILNDOM</th>-->
<!--            <th>ILNDOMQ</th>-->
<!--            <th>ILS</th>-->
<!--            <th>ILSQ</th>-->
<!--            <th>ISC</th>-->
<!--            <th>ISCQ</th>-->
<!--            <th>LNCI</th>-->
<!--            <th>LNLSGR</th>-->
<!--            <th>LNLSNET</th>-->
<!--            <th>NETINC</th>-->
<!--            <th>NETINCQ</th>-->
<!--            <th>SC</th>-->
        </tr>
        </thead>
        <tbody>
        {#each res.data as d}
            <tr>
<!--                <td>{d.data.ID}</td>-->
                <td>
                    <button class="btn btn-xs btn-primary">{FormatDate(d.data.REPDTE)}</button>
                </td>
<!--                <td>{d.data.REPYEAR}</td>-->
                <td>{d.data.NAME}</td>
                <td>{d.data.CITY}</td>
                <td>{d.data.FLDOFF}</td>
                <td>{d.data.ZIP}</td>
                <td>{d.data.STNAME}</td>
                <td>{d.data.ACTIVE}</td>
                <td>{d.data.CERT}</td>
                <td>{FormatCash(d.data.ASSET)} M</td>
                <td>{FormatCash(d.data.CHBAL)} M</td>
<!--                <td>{d.data.CHBALNI}</td>-->
<!--                <td>{d.data.CHFRB}</td>-->
<!--                <td>{d.data.DEP}</td>-->
<!--                <td>{d.data.EQ}</td>-->
<!--                <td>{d.data.FREPO}</td>-->
<!--                <td>{d.data.ICHBAL}</td>-->
<!--                <td>{d.data.ICHBALQ}</td>-->
<!--                <td>{d.data.IFREPO}</td>-->
<!--                <td>{d.data.IFREPOQ}</td>-->
<!--                <td>{d.data.ILNDOM}</td>-->
<!--                <td>{d.data.ILNDOMQ}</td>-->
<!--                <td>{d.data.ILS}</td>-->
<!--                <td>{d.data.ILSQ}</td>-->
<!--                <td>{d.data.ISC}</td>-->
<!--                <td>{d.data.ISCQ}</td>-->
<!--                <td>{d.data.LNCI}</td>-->
<!--                <td>{d.data.LNLSGR}</td>-->
<!--                <td>{d.data.LNLSNET}</td>-->
<!--                <td>{d.data.NETINC}</td>-->
<!--                <td>{d.data.NETINCQ}</td>-->
<!--                <td>{d.data.SC}</td>-->
            </tr>
        {/each}
        </tbody>
    </table>
{/await}

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
                fields: "ID,NAME,CITY,FLDOFF,ZIP,STNAME,ACTIVE,CERT,ASSET,CHBAL,CHBALNI,CHFRB,"+
                    "DEP,EQ,FREPO,ICHBAL,ICHBALQ,IFREPO,IFREPOQ,ILNDOM,ILNDOMQ,ILS,ILSQ,ISC,ISCQ,"+
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
            console.log(response.data)
            return response.data;
        } else {
            throw new Error("Could not retrieve the data.");
        }
    }

    let financials = GetFinancials()
</script>