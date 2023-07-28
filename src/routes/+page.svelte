<script>
    import Match from './Match.svelte';

    import '../app.css';
</script>

<header>
    <h1>Header</h1>
    <p>Header content</p>
</header>

<main>
    <Match />
</main>

<footer>
    <h1>Footer</h1>
    <p>Footer content</p>
</footer>

<style>
    main {
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        place-items: center;
    }
</style>