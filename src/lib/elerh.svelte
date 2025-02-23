<script>
    import { onMount } from 'svelte'
    var current_url = ''
    onMount(async () => {
        current_url = window.location.href
    })
</script>
<div class="c">
    <div class="image"><img src="{current_url}/myface.jpg" alt="MyFace"></div>
    <div class="elerh">
        <h2>Németh Tamás</h2>
        <p>adjunktus</p>
        <p><a href="https://inf.u-szeged.hu/" target="_blank">SZTE TTIK Informatikai Intézet</a></p>
        <p><a href="https://inf.u-szeged.hu/fcs" target="_blank">Számítástudomány Alapjai Tanszék</a></p>
        <p>Szeged, Tisza Lajos krt. 103. (H-6701 Szeged, Postafiók 652.)</p>
        <p class="email">t n e m e t h  @   i n f . u - s z e g e d . h u</p>
    </div>
</div>
<style>
    .email {
        letter-spacing: -2px;
        user-select: none;
    }
    .c {
        display: flex; 
    }
    .elerh {
        text-align: left;
        margin-left: 20px;
        font-size: 18px;
    }
    .image {
        margin-left: 20px;
        margin-right: 20px;
    }
    .image img {
        width: 200px;
        border-radius: 20px;
        border: solid 10px white;
    }
    h2 {
        padding-top: 10px;
    }
    p {
        padding: 0px;
        margin: 0px;
        margin-top: 5px;
    }
    a {
        color: blanchedalmond;
    }
    a:visited {
        color: rgb(201, 183, 156);
    }
    a:hover {
        color: #535bf2;
    }

</style>
