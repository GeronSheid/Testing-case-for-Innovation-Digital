<script lang="ts">
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
    // let notificationText = 'Your proposal was succesefully sended. Thank you for your opinion, this is very important for us. We will answer you as soon as possible.';

    let notificationData = {
        title: '',
        text: '',
        status: false
    }
    const sendData = async () => {
        let data = {
            name,
            company,
            email,
            phone,
            subject,
            message
        }
        const response = await fetch('url', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(data),
        });

        if (response.ok) {
            console.log('Данные успешно отправлены!');
            notificationData.title = 'Message sended'
            notificationData.text = 'Your proposal was succesefully sended. Thank you for your opinion, this is very important for us. We will answer you as soon as possible.'
            notificationData.status = true

        } else {
            console.error('Произошла ошибка при отправке данных.');
            notificationData.title = 'Something went wrong'
            notificationData.text = 'Try to send another message or please try again later'
            notificationData.status = false
        }
    }
    
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
            checkboxError = ' Checkbox is required'
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
        sendData()
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
        notificationTitle={notificationData.title}
        notificationText={notificationData.text}
        notificationStatus={notificationData.status}
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
                    I accept <a target="_blank" href="https://digitalpartnersglobal.com/privacy_policy?l=en">Terms and Privacy Policy</a>
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
        gap: 0.6rem;
        color: $textMain;
        line-height: 120%;
        text-align: center;

        &__wrapper {
            margin-bottom: 4.8rem;
            padding: 2.22rem 2.5rem;
            background-color: $backgroundMain;
            box-shadow: $shadow;
            border-radius: 27px;
        }

        &__header{
            max-width: 238px;
            span {
                color: $textSecondary;
                font-size: 0.83rem;
                font-weight: 300;
            }
        }

        &__inputs {
            max-width: 300px;
            width: 120%;
            display: flex;
            flex-direction: column;
            gap: 2.11rem;
        }

        &__confidential {
            position: relative;
            max-width: 263px;
            
        }

        &__checkbox-row {
            display: flex;
            align-items: center;
            gap: 0.66rem;
            padding: 1.44rem 0;
            & > label {
                flex: 1 0 auto;
                font-size: 0.66rem;
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
            font-size: 0.66rem;
            color: $textError;
        }
    }
</style>