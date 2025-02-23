<script>
import markdownit from 'markdown-it'
import { onMount } from 'svelte'
const md = markdownit()
let current_url = '/inf_honlap2/'
var result = $state('')
var height = $state(window.innerHeight)
onMount(async () => {
    current_url = window.location.href
    var file = await fetch(current_url + '/md/_cv.md')
    result = md.render(await file.text())    
})
</script>
<svelte:window bind:innerHeight={height} />
<code style="height: {height - 120}px;">
    {@html result}
</code>

