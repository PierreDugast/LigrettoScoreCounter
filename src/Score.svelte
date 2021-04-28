<script>
    export let history;


    function compute() {
        let total = 0;
        history = history.match(/[+\−]*(\.\d+|\d+(\.\d+)?)/g) || [];
        while (history.length) {
            total += parseFloat(history.shift());
        };
        return total;
    };

    $: score = compute();
</script>
    
<p>{score}</p>













