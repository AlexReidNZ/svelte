<script>
    export let pageName = "";
</script>

<a href={pageName}><section><p>{pageName}</p></section></a>

<style>
    section {
        width: 10vw;
        height: 10vh;
        border-radius: 10px;
        background-color: var(--darkColour);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    section:hover {
        transform: scale(1.2);
        transition-duration: 500ms;
    }
    a {
        color: var(--highlightText);
        text-decoration: underline;
        text-decoration-color: var(--highlightText);
    }
    a:visited {
        color: var(--highlightText);
        text-decoration: underline;
        text-decoration-color: var(--highlightText);
    }
    a:hover {
        color: var(--mainText);
    }
</style>
