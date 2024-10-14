<script lang="ts">
    import '../../variables.scss';

    import Button from "./button.svelte";
    import Checkbox from "./checkbox.svelte";
    import Input from "./input.svelte";
    import Notification from "./Notification.svelte";

    let name: string = '';
    let company: string = '';
    let email: string = '';
    let phone: string = '';
    let subject: string = '';
    let message: string = '';
    let isChecked = false;

    let nameError: string = '';
    let companyError: string = '';
    let emailError: string = '';
    let phoneError: string = '';
    let checkboxError: string = '';

    let notificationVisible: boolean = false;
    let notificationText = 'Your proposal was succesefully sended. Thank you for your opinion, this is very important for us. We will answer you as soon as possible.';

    
    const onValidate = () => {
        let isValid = true;
        if(name.trim().length === 0) {
            nameError = 'Please enter your name'
            isValid = false
        } else {
            nameError = ''
        }

        if(company.trim().length === 0) {
            companyError = 'Please enter your company'
            isValid = false
        } else {
            nameError = ''
        }

        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if(!emailRegex.test(email) && email.trim().length === 0) {
            emailError = 'Please enter a valid email adress'
            isValid = false
        } else {
            emailError = ''
        }

        const phoneRegex = /^\+?(375|7|996|374|994|998|992)(\s?\d{1,3})?(\s?\d{3}|\d{3})(\s?\d{2}|\d{2}){2}$|^\d{7,15}$/;
        if(!phoneRegex.test(phone) && phone.trim().length === 0) {
            phoneError = 'Please enter a valid phone number'
            isValid = false
        } else {
            phoneError = ''
        }

        if(!isChecked) {
            checkboxError = 'Please check our rules'
            isValid = false
        } else {
            checkboxError = ''
        }

        return isValid;
    }

    const onSubmit = () => {
        let validation = onValidate()
        if(!validation) {
            return
        }
        //тут должен быть fetch, но куда отправлять то?
        console.log(name, company, email, phone, message, subject)
        notificationVisible = true;
        setTimeout(() => {
            notificationVisible = false;
        }, 3000);
        name = ''
        company = ''
        email = ''
        phone = ''
        message = ''
        subject = ''
        isChecked = false
        console.log(notificationVisible)
    }
    
    const closeNotification = () => {
        notificationVisible = false;
    }
</script>

<div class="form__wrapper">
    <Notification
        isVisible={notificationVisible}
        notificationText={notificationText}
        onClose={closeNotification}
    />
    <form class="form" on:submit|preventDefault={onSubmit}>
        <div class="form__header">
            <p>For business enquiries please use the form below</p>
            <span>*Required</span>
        </div>
        <div class="form__inputs">
            <Input 
                value={name}
                onInput={value => {name = value;}}
                name='name'
                label='Name' 
                type='text' 
                isRequired
                error={nameError}
            />
            <Input
                value={company}
                onInput={value => {company = value;}}
                name='company'
                label='Company' 
                type='text' 
                isRequired
                error={companyError}
            />
            <Input
                value={email}
                onInput={value => {email = value;}}
                name='email'
                label='E-mail' 
                type='email' 
                isRequired
                error={emailError}
            />
            <Input
                value={phone}
                onInput={value => {phone = value;}}
                name='phone'
                label='Phone' 
                type='phone'
                isRequired
                error={phoneError}
            />
            <Input
                value={subject}
                onInput={value => {subject = value;}}
                name='subject'
                label='Subject' 
                type='text' 
            />
            <Input
                value={message}
                onInput={value => {message = value;}}
                name='message'
                label='Message' 
                type='message' 
            />
        </div>
        <div class="form__confidential">
            <div class="form__checkbox-row">
                <Checkbox 
                    name='confidential'
                    bind:isChecked            
                />
                <label for="form-confidential">
                    I accept <a href="#">Terms and Privacy Policy</a>
                </label>
            </div>
            {#if checkboxError}
                <span class="form__error">{checkboxError}</span>
            {/if}
        </div>
        <Button
            type='default'
            onClick={() => onSubmit()}
        >
        Send
        </Button>
    </form>
</div>

<style lang="scss">

    $backgroundMain: #171929;
    $shadow: 0 0 50px #000000bb;
    $textMain: #fff;
    $textSecondary: #797EA3;
    $textAccent: #B9BEE5;
    $textError: #FF1800;


    .form {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 10px;
        color: $textMain;
        font-size: 18px;
        line-height: 120%;
        text-align: center;

        &__wrapper {
            margin-bottom: 87px;
            padding: 40px 45px;
            background-color: $backgroundMain;
            box-shadow: $shadow;
            border-radius: 27px;
        }

        &__header{
            max-width: 238px;
            span {
                color: $textSecondary;
                font-size: 15px;
                font-weight: 300;
            }
        }

        &__inputs {
            max-width: 300px;
            width: 120%;
            display: flex;
            flex-direction: column;
            gap: 38px;
        }

        &__confidential {
            position: relative;
            max-width: 263px;
            
        }

        &__checkbox-row {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 26px 0;
            & > label {
                flex: 1 0 auto;
                font-size: 15px;
                font-weight: 300;
                color: $textSecondary;
                & > a {
                    color: $textAccent;
                }
            }
        }

        &__error {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;
            font-size: 12px;
            color: $textError;
        }
    }
</style>