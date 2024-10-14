<script>
    import Form from "./components/form.svelte";
    import '../global.scss';
    
</script>

<div class="wrapper">
    <div class="container">
        <h1>Hello</h1>
        <Form/>
        
    </div>
</div>
<style lang="scss">
    .wrapper {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        color: #fff;
        text-align: center;
        overflow: auto;
        background-image: url('Desktop.jpg');
        background-repeat: no-repeat;
        background-size: cover;
    }
    .container {
        height: auto;
        max-width: 410px;
        margin: 0 auto;
        padding: 0 10px;

    & > h1 {
        font-size: 55;
        margin-top: 87px;
        margin-bottom: 27px;
    }
    }
</style>
