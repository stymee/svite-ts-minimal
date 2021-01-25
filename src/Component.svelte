<script lang="ts">
    import {clickCount, clickTime} from './click.store';
    import dayjs from 'dayjs';
    import {onMount} from 'svelte';
    import queryString from 'query-string';

    export let location;
    export let id: string = 'nothing';

    let hello = '';
    let date = new Date();
    let params;

    function onClick() {
        $clickCount++;
        $clickTime = dayjs(Date.now()).format('ddd M/D/YY h:mm:ss.SSS a');
    }

    onMount(() => {
        $clickCount = parseInt(id);
        console.log('location', location);
        console.log('search', location?.search);
        console.log('query params', queryString.parse(location?.search));
        params = queryString.parse(location?.search);
        hello = params?.hello;
        date = dayjs(params?.date).toDate();
    });
</script>

<button on:click={onClick}>{$clickCount} Clicks!!!</button>
<p>{$clickTime}</p>
<p>hello={hello}</p>
<p>date={dayjs(date).format('ddd YYYY-MM-DD hh:mm:ss.SSS a')}</p>

<style>
</style>
