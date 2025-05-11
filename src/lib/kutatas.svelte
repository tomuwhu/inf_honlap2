<script>
    import markdownit from 'markdown-it'
    import { onMount } from 'svelte'
    const md = markdownit()
    let current_url = '.'
    var result = $state('')
    var height = $state(window.innerHeight)
    onMount(async () => {
        var file = await fetch(current_url + '/md/aapl.md')
        result = md.render(await file.text())    
    })
    </script>
    <svelte:window bind:innerHeight={height} />
    <code style="height: {height - 80}px;">
        {@html result}
    </code>
    <style>
        code {
            width: 800px;
            padding-left: 10px;
        }
        :global(p) {
            padding: 10px;
        }
        :global(em) {
            color: rgb(210, 166, 166);
        }
        :global(strong){
            color: rgb(225, 233, 193);
        }
        :global(a) {
            font-weight: bold;
        }
    </style>