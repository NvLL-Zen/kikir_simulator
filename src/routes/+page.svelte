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
    <h1>Gacha Simulator</h1>
    <div>
        {#each pulled as item}
            <span class={getRarityClass(item)}>{item}</span>
        {/each}
    </div>
    <div>current pity: {pity}</div>
    <div class="buttpnContainer">
    <button onclick={pull_1}>1X</button>
    <button onclick={pull_10}>10X</button>
    </div>
    
</div>