<script>
import markdownit from 'markdown-it'
import { onMount } from 'svelte'
const md = markdownit()
var result = $state('')
var height = $state(window.innerHeight)
onMount(async () => {
    var file = await fetch('/md/_cv.md')
    result = md.render(await file.text())    
})
</script>
<svelte:window bind:innerHeight={height} />
<code style="height: {height - 120}px;">
    {@html result}
</code>

