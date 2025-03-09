<script>
    import "../styles/global.css"

    let pity = $state(0)
    let chance = 6
    let pulled = $state([])

    const rng = (num) => {
        return Math.floor(Math.random() * num) + 1;
    }

    const gacha = () => {
        let gacha_item = rng(1000)
        if (gacha_item <= 6 ) {
            gacha_item = 5
        } else if (gacha_item <= 100) {
            gacha_item = 4
        } else {
            gacha_item = 3
        }
        if (pity >= 80) {
            pity = pity%10 
            gacha_item = 5
        }
        return gacha_item
    }

    const pull_1 = () => {
        pulled = []
        pulled.push(`${gacha()}*`)
        pity += 1
    }

    const pull_10 = () => {
        pulled = []
        for(let i = 0; i < 10; i++){
        pulled.push(`${gacha()}*`)
        }

        pity += 10
        
    }

    const getRarityClass = (item) => {
        if (item.startsWith('5')) return 'rarity-5';
        if (item.startsWith('4')) return 'rarity-4';
        if (item.startsWith('3')) return 'rarity-3';
        return '';
    }

</script>

<div class="pageContainer">
    <div class="mainContainer">
    <h1>Gacha Simulator</h1>
    <div class="cardsContainer" >
        <div class="rows">
            {#each pulled.slice(0,3) as item}
            <span class="Cards {getRarityClass(item)}">{item}</span>
        {/each}
        </div>
        <div class="rows">
            {#each pulled.slice(3,7) as item}
            <span class="Cards {getRarityClass(item)}">{item}</span>
        {/each}
        </div>
        <div class="rows">
            {#each pulled.slice(7, 11) as item}
            <span class="Cards {getRarityClass(item)}">{item}</span>
        {/each}
        </div>
        
    </div>
    <div class="pityCounter">current pity: {pity}</div>
    <div class="buttonContainer">
    <button onclick={pull_1}>1X</button>
    <button onclick={pull_10}>10X</button>
    </div>
</div>
    
</div>