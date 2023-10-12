<script>
    let heroTextOptions = [
        "there have been pawprints spotted on the ceiling",
        "one of these rooms has yarn all over the floor",
        "mysterious scratch marks cover the wallpapers",
        "don't let it fall asleep on you ~ or you'll never get up",
        "you hear a faint purring from behind the windows",
        "those items weren't supposed to be on the floor",
        "it feels like you are being watched (from under the furniture)",
        "meow"
    ];
    let heroText = heroTextOptions[Math.floor(Math.random()*heroTextOptions.length)] + "...";
</script>

<div class="hero">
    <div class="filmGrain"></div>
    <div class="imgBackground">
        <video loop autoplay muted>
            <source src="/img/willow-street.mp4" type="video/mp4">
        </video>
    </div>
    <p>{heroText}</p>
</div>