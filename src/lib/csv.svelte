<script>
import markdownit from 'markdown-it'
import { onMount } from 'svelte'
const md = markdownit()
let current_url = '.'
var result = $state('')
var height = $state(window.innerHeight)
onMount(async () => {
    console.log(current_url + '/md/_cv.md')
    var file = await fetch(current_url + '/md/aacv.md')
    result = md.render(await file.text())    
})
</script>
<svelte:window bind:innerHeight={height} />
<code style="height: {height - 80}px;">
    {@html result}
</code>

