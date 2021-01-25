<script lang="ts">
    import dayjs from 'dayjs';
    import {onMount} from 'svelte';
    import {Router, Route} from 'svelte-routing';
    import Component from './Component.svelte';

    const world = 'world'; // edit world and save to see hmr update

    let nowTime: string = 'getting time...';

    const url = '';
    const basepath = import.meta.env.PROD ? import.meta.env.VITE_BASE : '/';

    onMount(() => {
        console.log('PROD', import.meta.env.PROD);
        console.log('VITE_BASE', import.meta.env.VITE_BASE);
        console.log('using basepath=', basepath);


        nowTime = dayjs(Date.now()).format('ddd M/D/YY h:mm:ss.SSS a');

        const interval = setInterval(() => {
            nowTime = dayjs(Date.now()).format('ddd M/D/YY h:mm:ss.SSS a');
        }, 100);
        return () => {
            clearInterval(interval);
        };
    });
</script>

<h1>Hello {world} !!!!</h1>
<p>Open App.svelte in your editor and change something to see HMR in action</p>
<p>{nowTime}</p>
<Router {url} {basepath}>
    <Route path="/">
        <p>Home!</p>
    </Route>
    <!-- must use the non-slot method if you want to pass route param (id) and query params (location) -->
    <Route path="click/:id" component={Component}/>
    <!-- can use the slot method below just to show something else -->
    <Route path="/about">
        <p>About!</p>
    </Route>
    <Route>
        <p>404: nOt fOuNd</p>
    </Route>
</Router>

<style>
    h1 {
        color: orange; /* change color an save to see hmr update */
    }
</style>
