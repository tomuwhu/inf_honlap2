<script>
    import markdownit from 'markdown-it'
    const md = markdownit()
    var height = $state(window.innerHeight)
    var selected_subject = $state(0)
    var selected_year = $state(0)
    var result = $state('')
    const list = $state([
        {name: '', year: [], md: []},
        {name: 'Algoritmusok és adatszerkezetek I.', years: [2024, '2009-2014'], mds: ['alga1', 'alga1_old']},
        {name: 'Algoritmizálás', years: ['2012-2024'], mds: ['algo']},
        {name: 'Elemi informatika I.', years: ['2016-2020'], mds: ['eli1']},
        {name: 'Elemi informatika II.', years: ['2016-2020'], mds: ['eli2']},
        {name: 'Informatikai alkalmazások', years: ['2016-2022'], mds: ['infalk']},
        {name: 'Oktatást támogató informatikai rendszerek', years: ['2016-2024'], mds: ['otir']},
        {name: 'Programozási versenyek feladatainak megoldása', years: ['2016-2024'], mds: ['pmsz']},
    ])
    var ssyears = $derived(list[selected_subject].years)
    var ssmds = $derived(list[selected_subject].md)
    let current_url = '/inf_honlap2'
    const getmd = async () => {       
        var file = await fetch(current_url + '/md/' + list[selected_subject]?.mds[selected_year] + '.md')
        result = md.render(await file.text())
    }
</script>
<svelte:window bind:innerHeight={height} />
<div>
    <div class="selectrow">
        <select class="ui fluid dropdown" bind:value={selected_subject}
            onchange={getmd}>
            {#each list as item, index}
                <option value={index}>{item.name}</option>
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
</div>
<div class="ui divider"></div>
<code style="height: {height - 120}px;">
    {@html result}
</code>
<style>
code {
    width: 900px;
}
.selectrow {
    display: inline-block;
    width: 300px;
}
.selectrow2 {
    display: inline-block;
    width: 100px;
    text-align-last: right;
}
</style>