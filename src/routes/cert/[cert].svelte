<h1>Reports for Cert: {cert}</h1>
<hr>
{#await financials}
    <p>...loading</p>
{:then res}
    <div class="row mb-5">
        <div class="col-6">
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
        <div class="col">
            <h2>Raw Data</h2>
            <table class="table table-striped table-sm">
                <thead>
                <tr>
                    <th>API Field</th>
                    <th>Field Description</th>
                    <th>Report Value</th>
                </tr>
                </thead>
                <tbody>
                <tr>
                    <td>ID</td>
                    <td>Cert + Report Date ID</td>
                    <td class="text-end">{selected.ID}</td>
                </tr>
                <tr>
                    <td>REPDTE</td>
                    <td>Report Date</td>
                    <td class="text-end">{FormatDate(selected.REPDTE)}</td>
                </tr>
                <tr>
                    <td>REPYEAR</td>
                    <td>Report Year</td>
                    <td class="text-end">{selected.REPYEAR}</td>
                </tr>
                <tr>
                    <td>NAME</td>
                    <td>Bank Name</td>
                    <td class="text-end">{selected.NAME}</td>
                </tr>
                <tr>
                    <td>CITY</td>
                    <td>City</td>
                    <td class="text-end">{selected.CITY}</td>
                </tr>
                <tr>
                    <td>FLDOFF</td>
                    <td>FDIC Field Office</td>
                    <td class="text-end">{selected.FLDOFF}</td>
                </tr>
                <tr>
                    <td>ZIP</td>
                    <td>Zip Code</td>
                    <td class="text-end">{selected.ZIP}</td>
                </tr>
                <tr>
                    <td>STNAME</td>
                    <td>State Name</td>
                    <td class="text-end">{selected.STNAME}</td>
                </tr>
                <tr>
                    <td>ACTIVE</td>
                    <td>Active</td>
                    <td class="text-end">{selected.ACTIVE}</td>
                </tr>
                <tr>
                    <td>CERT</td>
                    <td>FDIC Certificate #</td>
                    <td class="text-end">{selected.CERT}</td>
                </tr>
                <tr>
                    <td>ASSET</td>
                    <td>Total Assets</td>
                    <td class="text-end">{selected.ASSET}</td>
                </tr>
                <tr>
                    <td>CHBAL</td>
                    <td>Cash & Due from Depository Institution</td>
                    <td class="text-end">{selected.CHBAL}</td>
                </tr>
                <tr>
                    <td>CHBALNI</td>
                    <td>Non-Interest-Bearing Cash & Due</td>
                    <td class="text-end">{selected.CHBALNI}</td>
                </tr>
                <tr>
                    <td>CHFRB</td>
                    <td>Balance Due from FRB</td>
                    <td class="text-end">{selected.CHFRB}</td>
                </tr>
                <tr>
                    <td>DEP</td>
                    <td>Total Deposits</td>
                    <td class="text-end">{selected.DEP}</td>
                </tr>
                <tr>
                    <td>EQ</td>
                    <td>Total Equity Capital</td>
                    <td class="text-end">{selected.EQ}</td>
                </tr>
                <tr>
                    <td>FREPO</td>
                    <td>Fed Funds Sold</td>
                    <td class="text-end">{selected.FREPO}</td>
                </tr>
                <tr>
                    <td>ICHBAL</td>
                    <td>Cash Due from Depositories</td>
                    <td class="text-end">{selected.ICHBAL}</td>
                </tr>
                <tr>
                    <td>ICHBALQ</td>
                    <td>Cash Due from Depositories (Quarterly)</td>
                    <td class="text-end">{selected.ICHBALQ}</td>
                </tr>
                <tr>
                    <td>IFREPO</td>
                    <td>Fed Funds Sold</td>
                    <td class="text-end">{selected.IFREPO}</td>
                </tr>
                <tr>
                    <td>IFREPOQ</td>
                    <td>Fed Funds Sold (Quarterly)</td>
                    <td class="text-end">{selected.IFREPOQ}</td>
                </tr>
                <tr>
                    <td>ILNDOM</td>
                    <td>Loan Income-Dom</td>
                    <td class="text-end">{selected.ILNDOM}</td>
                </tr>
                <tr>
                    <td>ILNDOMQ</td>
                    <td>Loan Income-Dom (Quarterly)</td>
                    <td class="text-end">{selected.ILNDOMQ}</td>
                </tr>
                <tr>
                    <td>ILS</td>
                    <td>Lease Income</td>
                    <td class="text-end">{selected.ILS}</td>
                </tr>
                <tr>
                    <td>ILSQ</td>
                    <td>Lease Income (Quarterly)</td>
                    <td class="text-end">{selected.ILSQ}</td>
                </tr>
                <tr>
                    <td>ISC</td>
                    <td>Total Security Income</td>
                    <td class="text-end">{selected.ISC}</td>
                </tr>
                <tr>
                    <td>ISCQ</td>
                    <td>Total Security Income (Quarterly)</td>
                    <td class="text-end">{selected.ISCQ}</td>
                </tr>
                <tr>
                    <td>LNCI</td>
                    <td>C&I Loans</td>
                    <td class="text-end">{selected.LNCI}</td>
                </tr>
                <tr>
                    <td>LNLSGR</td>
                    <td>Total Loans & Leases</td>
                    <td class="text-end">{selected.LNLSGR}</td>
                </tr>
                <tr>
                    <td>LNLSNET</td>
                    <td>Net Loans & Leases</td>
                    <td class="text-end">{selected.LNLSNET}</td>
                </tr>
                <tr>
                    <td>NETINC</td>
                    <td>Net Income1</td>
                    <td class="text-end">{selected.NETINC}</td>
                </tr>
                <tr>
                    <td>NETINCQ</td>
                    <td>Net Income1 (Quarterly)</td>
                    <td class="text-end">{selected.NETINCQ}</td>
                </tr>
                <tr>
                    <td>SC</td>
                    <td>Securities</td>
                    <td class="text-end">{selected.SC}</td>
                </tr>
                <tr>
                    <td>INTINC</td>
                    <td>Total Interest Income</td>
                    <td class="text-end">{selected.INTINC}</td>
                </tr>
                <tr>
                    <td>INTINQ</td>
                    <td>Total Interest Income (Quarterly)</td>
                    <td class="text-end">{selected.INTINQ}</td>
                </tr>
                <tr>
                    <td>(computed)</td>
                    <td>Net Loans & Leases</td>
                    <td class="text-end">{selected.ILNDOM + selected.ILS}</td>
                </tr>
                <tr>
                    <td>(computed)</td>
                    <td>Net Loans & Leases (Quarterly)</td>
                    <td class="text-end">{selected.ILNDOMQ + selected.ILSQ}</td>
                </tr>
                <tr>
                    <td>(computed)</td>
                    <td>Cash and due from Depositories2</td>
                    <td class="text-end">{selected.CHBAL - selected.CHBALNI}</td>
                </tr>
                </tbody>
            </table>
        </div>

<!--        <div class="col">-->
<!--            <h3>Earning Assets</h3>-->
<!--            <table class="table table-sm-table-striped">-->
<!--                <thead>-->
<!--                <tr>-->
<!--                    <td></td>-->
<!--                    <td></td>-->
<!--                    <td>% of Total Assets</td>-->
<!--                    <td>Interest Income 1</td>-->
<!--                    <td>Yield</td>-->
<!--                </tr>-->
<!--                </thead>-->
<!--                <tbody>-->
<!--                <tr>-->
<!--                    <th>Cash and Due from Depositories</th>-->
<!--                    <td>{FormatCash(calc.earningAssets.cashDueDepositories[0].toFixed(1))}</td>-->
<!--                    <td>{(calc.earningAssets.cashDueDepositories[1] * 100).toFixed(1)}%</td>-->
<!--                    <td>{(calc.earningAssets.cashDueDepositories[2]).toFixed(1)}</td>-->
<!--                    <td>{(calc.earningAssets.cashDueDepositories[3]*100).toFixed(2)}%</td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>Fed Funds Sold</th>-->
<!--                    <td>{calc.earningAssets.fedFundsSold[0]}</td>-->
<!--                    <td>{(calc.earningAssets.fedFundsSold[1] * 100).toFixed(1)}%</td>-->
<!--                    <td>{calc.earningAssets.fedFundsSold[2]}</td>-->
<!--                    <td>{calc.earningAssets.fedFundsSold[3]}</td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>Net Loans & Leases</th>-->
<!--                    <td>{calc.earningAssets.netLoansLeases[0]}</td>-->
<!--                    <td>{calc.earningAssets.netLoansLeases[1]}</td>-->
<!--                    <td>{calc.earningAssets.netLoansLeases[2]}</td>-->
<!--                    <td>{calc.earningAssets.netLoansLeases[3]}</td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>Securities</th>-->
<!--                    <td>{calc.earningAssets.securities[0]}</td>-->
<!--                    <td>{calc.earningAssets.securities[1]}</td>-->
<!--                    <td>{calc.earningAssets.securities[2]}</td>-->
<!--                    <td>{calc.earningAssets.securities[3]}</td>-->
<!--                </tr>-->
<!--                <tr class="border-1">-->
<!--                    <th>Total</th>-->
<!--                    <td>{calc.earningAssets.total[0]}</td>-->
<!--                    <td>{calc.earningAssets.total[1]}</td>-->
<!--                    <td>{calc.earningAssets.total[2]}</td>-->
<!--                    <td>{calc.earningAssets.total[3]}</td>-->
<!--                </tr>-->
<!--                </tbody>-->
<!--            </table>-->
<!--        </div>-->
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

    // $: calc = (function() {
    //     let out = {};
    //     if (selected === null) {
    //         return out;
    //     }
    //
    //     function percentOfAssets(val) {
    //         const assets = selected.ASSET / 1000;
    //         return val / assets;
    //     }
    //
    //     out.earningAssets = {};
    //     out.earningAssets.cashDueDepositories = [];
    //     out.earningAssets.cashDueDepositories[0] = (selected.CHBAL - selected.CHBALNI) / 1000;
    //     out.earningAssets.cashDueDepositories[1] = percentOfAssets(out.earningAssets.cashDueDepositories[0]);
    //     out.earningAssets.cashDueDepositories[2] = (selected.ICHBAL/1000 * 1.33333333333333);
    //     out.earningAssets.cashDueDepositories[3] = (out.earningAssets.cashDueDepositories[2] / out.earningAssets.cashDueDepositories[0]);
    //
    //     out.earningAssets.fedFundsSold = [];
    //     out.earningAssets.fedFundsSold[0] = selected.IFREPO;
    //     out.earningAssets.fedFundsSold[1] = percentOfAssets(out.earningAssets.fedFundsSold[0]);
    //     out.earningAssets.fedFundsSold[2] = (selected.ICHBAL/1000 * 1.33333333333333);
    //     out.earningAssets.fedFundsSold[3] = (out.earningAssets.fedFundsSold[2] / out.earningAssets.fedFundsSold[0]);
    //
    //     out.earningAssets.netLoansLeases = [];
    //     out.earningAssets.netLoansLeases[0] = selected.LNLSNET / 1000;
    //
    //     out.earningAssets.securities = [];
    //     out.earningAssets.securities[0] = selected.SC / 1000;
    //
    //     out.earningAssets.total = [];
    //     out.earningAssets.total[0] =
    //         out.earningAssets.cashDueDepositories[0] +
    //         out.earningAssets.fedFundsSold[0] +
    //         out.earningAssets.netLoansLeases[0] +
    //         out.earningAssets.securities[0];
    //
    //     return out;
    // })();

    // $: calc = (function() {
    //     const x = selected;
    //     let out = {};
    //     if (!x) {
    //         return out;
    //     }
    //
    //     out.ea.cadfd = x.CHBAL - x.CHBALNI;
    //     out.ea.cadfdP = out.ea.cadfd / x.ASSET;
    //
    //     return out;
    // })();

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
                    "LNCI,LNLSGR,LNLSNET,NETINC,NETINCQ,SC,REPDTE,REPYEAR,INTINC,INTINQ",
                filters: "CERT:" + cert + " AND ACTIVE:1",
                format: "json",
                limit: "5000",
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