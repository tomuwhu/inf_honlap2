<script>
    import markdownit from 'markdown-it'
    const md = markdownit()
    var height = $state(window.innerHeight)
    var selected_subject = $state(0)
    var selected_year = $state(0)
    var result = $state('')
    const list = $state([
        {name: 'Algoritmusok és adatszerkezetek I.', years: [2024, '2009-2014'], mds: ['alga1', 'alga1_old']},
        {name: 'Algoritmizálás', years: ['2012-2024'], mds: ['algo']},
        {name: 'Elemi informatika I.', years: ['2016-2020'], mds: ['eli1']},
        {name: 'Elemi informatika II.', years: ['2016-2020'], mds: ['eli2']},
        {name: 'Informatikai alkalmazások', years: ['2016-2022'], mds: ['infalk']},
        {name: 'Oktatást támogató informatikai rendszerek', years: ['2016-2024'], mds: ['otir']},
        {name: 'Programozási versenyek feladatainak megoldása', years: ['2016-2024'], mds: ['pmsz']},
        {name: 'Webes technológiák - SvelteKit/Drizzle/Turso/Lucia', years: ['nem akítv'], mds: ['wt']},
        {name: 'Elemi algoritmusok és adatstruktúrák alkalmazása a szoftverfejlesztésben', years: ['tervezett: 2025 ősz'], mds: ['dsinszofteng']},
        {name: 'Elemi algoritmusok és programozási eszközök a közoktatásban', years: ['Új tanárképzős tárgy'], mds: ['algandprogakn']},
        {name: 'Brython', years: ['Új tanárképzős tárgy'], mds: ['brython']},
    ])
    var ssyears = $derived(list[selected_subject - 1].years)
    let current_url = '/inf_honlap2'
    const getmd = async () => {       
        var file = await fetch(current_url + '/md/' + list[selected_subject-1]?.mds[selected_year] + '.md')
        result = md.render(await file.text())
    }
</script>
<svelte:window bind:innerHeight={height} />
{#if selected_subject > 0}
<div>
    <div class="selectrow">
        <select class="ui fluid dropdown" bind:value={selected_subject}
            onchange={() => {
                selected_year = 0
                getmd()
            }}>
            {#each list as item, index}
                <option value={index+1}>{item.name}</option>
            {/each}
        </select>
    </div>
    <div class="selectrow2" onchange={getmd}>
        <select class="ui fluid dropdown" bind:value={selected_year}>
            {#each ssyears as year, key}
                <option value={key}>{year}</option>
            {/each}
        </select>
    </div>
    <button onclick={() => {
        selected_year = 0
        selected_subject = 0
    }} class="ui small blue button">x</button>
</div>
<div class="ui divider"></div>
<code style="height: {height - 140}px;">
    {@html result}
</code>
{:else}
<div>
    <h2>Oktatott tárgyak</h2>
    <table class="ui table x">
    <thead>
        <tr>
            <th>Neve</th>
            <th>Szemeszter</th>
        </tr>
    </thead>
    <tbody>
    {#each list as item, index}
        <tr><td>{item.name}</td><td>
            {#each item.years as year}
                <button class="ui blue small button year"
                onclick={() => {
                    selected_subject = index + 1
                    selected_year = item.years.indexOf(year)
                    getmd()
                }}>{year}</button>
            {/each}
        </td></tr>
    {/each}
    </tbody>
    </table>
</div>
{/if}
<style>
table.x {
    margin: auto;
    display: table;
    max-width: 800px;
    min-width: 50%;
}
button.year {
    padding: 5px;
    margin: -10px 5px;
}
code {
    width: 900px;
    user-select: all;
}
.selectrow {
    display: inline-block;
    width: 300px;
}
.selectrow2 {
    display: inline-block;
    width: 220px;
    text-align-last: right;
}
:global(img) {
    width: 100px;
    background-color: aliceblue;
}
</style>