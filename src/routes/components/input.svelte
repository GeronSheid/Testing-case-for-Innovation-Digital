<script lang="ts">
    export let type: string = 'text'
    export let label: string | null
    export let name: string
    export let isRequired: boolean = false
    export let value: string
    export let onInput: (value: string) => void;
    export let error: string | null = ''

    const handleInput = (event: Event) => {
        const target = event.target as HTMLInputElement
        onInput(target.value)
    }
</script>

<div class="customInput">
    {#if label}
        <label for={`form-${name}`}>{isRequired ? `${label}*` : label}</label>
    {/if}
    {#if type == 'text'}
        <input 
            bind:value={value}
            on:input={handleInput}
            type="text"
            id={`form-${name}`}
            name={name} 
            required={isRequired}
        >
    {:else if type == 'phone'}
        <input 
            bind:value={value}
            on:input={handleInput}
            type="tel"
            id={`form-${name}`}
            name={name} 
            required={isRequired}
        >
    {:else if type == 'email'}
        <input 
            bind:value={value}
            on:input={handleInput}
            type="tel"
            id={`form-${name}`}
            name={name} 
            required={isRequired}
        >
    {:else if type == 'message'}
        <textarea 
            bind:value={value}
            on:input={handleInput}
            id={`form-${name}`}
            name={name} 
            required={isRequired}
        ></textarea>
    {/if}
    {#if error}
        <span class="customInput__error">{error}</span>
    {/if}
</div>


<style lang="scss">
    $input-color: #797EA3;
    $transition: 0.3s ease-in-out;

    .customInput {
        display: flex;
        position: relative;
        flex-direction: column;
        color: $input-color;
        text-align: left;
        transition: color $transition;

        & > input {
            margin: 6px 0 5px 0;
            color: inherit;
            background-color: transparent;
            border: none;
            outline: none;
        }

        & > textarea {
            margin: 6px 0 5px 0;
            color: inherit;
            background-color: transparent;
            border: none;
            outline: none;
            overflow: hidden; //Надо будет решить вопрос по другому. Это костыль
            resize: none;
        }

        &::after {
                content: '';
                position: absolute;
                height: 1px;
                width: 100%;
                left: 0;
                bottom: 0;
                background-color: $input-color;
                transition: background-color $transition;
            }

    &:focus-within {
        color: #fff;
        &::after {
            background-color: #fff;
        }
    }

    &__error {
        position: absolute;
        left: 0;
        bottom: -50%;
        font-size: 12px;
        color: red;
    }
    }

    @media (any-hover: hover) {
        .customInput:hover {
            color: #fff;
            &::after {
                background-color: #fff;
            }
        }
    }
</style>