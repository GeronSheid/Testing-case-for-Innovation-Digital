<script>
    import Form from "./components/form.svelte";
</script>

<div class="wrapper">
    <div class="container">
        <h1>Hello</h1>
        <Form/>
    </div>
</div>

<style>
    .wrapper {
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
        background: url('Desktop.jpg') 0 0 / cover no-repeat;
        color: #fff;
        text-align: center;
    }
    .container {
        max-width: 410px;
        margin: 0 auto;
        padding: 0 10px;
    }
</style>
