<script>
    import Progressbar from "./progressbar.svelte";
    let totalseconds = 20;
    let secondsleft = totalseconds;
    let isrunning = false;
    $: progress = ((totalseconds - secondsleft) / totalseconds) * 100;

    function starttimer(){
        isrunning = true;
        const timer = setInterval(() => {
            secondsleft-=1;
            if(secondsleft==0){
                clearInterval(timer);
                isrunning=false;
                secondsleft=totalseconds;
            }
        }, 1000);
    }
</script>
<style>
    h2{
        margin: 0;
    }
    .start{
        background-color: rgb(154, 73, 70);
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled]{
    background-color: rgb(194, 194, 194);
    cursor: not-allowed;
    }
</style>
<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">
        Seconds Left: {secondsleft}
    </h2>
</div>
<Progressbar {progress}/>
<div bp="grid">
<button 
on:click={starttimer}
disabled={isrunning}
bp="offset-5@md 4@md 12@sm"
class="start">
Start
</button>
</div>




