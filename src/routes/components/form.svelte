<script>
    import Input from "./input.svelte";
</script>

<div class="form__wrapper">
    <form class="form" action="">
        <div class="form__header">
            <p>For business enquiries please use the form below</p>
            <span>*Required</span>
        </div>
        <div class="form__inputs">
            <Input 
                value={''}
                name='name'
                label='Name' 
                type='text' 
                isRequired
            />
            <Input
                value={''}
                name='company'
                label='Company' 
                type='text' 
                isRequired
            />
            <Input
                value={''}
                name='email'
                label='E-mail' 
                type='email' 
                isRequired
            />
            <Input
                value={''}
                name='phone'
                label='Phone' 
                type='phone' 
            />
            <Input
                value={''}
                name='subject'
                label='Subject' 
                type='text' 
            />
            <Input
                value={''}
                name='message'
                label='Message' 
                type='message' 
            />
        </div>
        
    </form>
</div>

<style lang="scss">
    .form {
        color: #fff;
        font-size: 18px;
        line-height: 120%;
        text-align: center;

        &__wrapper {
            padding: 40px 45px;
            background-color: #171929;
            box-shadow: 0 0 50px #000000bb;
            border-radius: 27px;
        }

        &__header{
            span {
                color: #797EA3;
                font-size: 15px;
                font-weight: 300;
            }
        }

        &__inputs {
            display: flex;
            flex-direction: column;
            gap: 38px;
        }
    }
</style>