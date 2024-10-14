<script lang="ts">
    export let isChecked: boolean = false;
    export let name: string;

    const toggleCheckbox = (event: MouseEvent | KeyboardEvent) => {
        if(event instanceof KeyboardEvent) {
            if(event.key === 'Enter' || event.key === ' ') {
                isChecked = !isChecked
            }
        }
        if(event.type === 'click') {
            isChecked = !isChecked;
        }    
    }
</script>

<div class="customCheckbox__wrapper">
    <input 
        type="checkbox"
        bind:checked={isChecked}
        id={`form-${name}`}
        name={name}
        aria-hidden="true"
        tabindex="-1"
    />
    <div 
        class={`customCheckbox ${isChecked ? 'customCheckbox_active' : null}`}
        role="checkbox"
        aria-checked={isChecked}
        on:click={toggleCheckbox}
        on:keydown={toggleCheckbox}
        tabindex="0"
    >
        {#if isChecked}
            <svg 
                width="15" 
                height="11" 
                viewBox="0 0 15 11" 
                fill="none" 
                xmlns="http://www.w3.org/2000/svg">
                <path 
                    opacity="0.7"
                    d="M14.5607 0.429557C13.9749 -0.143186 13.0254 -0.143186 12.4396 0.429557L5.24994 7.45867L2.56038 4.82963C1.97536 4.25689 1.02434 4.25689 0.439324 4.82963C-0.146441 5.40237 -0.146441 6.33079 0.439324 6.90353L4.18942 10.5703C4.48193 10.857 4.86593 11 5.24994 11C5.63395 11 6.01796 10.857 6.31047 10.5703L14.5607 2.50346C15.1464 1.93072 15.1464 1.0023 14.5607 0.429557Z"
                    fill="currentColor"/>
            </svg>
        {/if}
    </div>
</div>

<style lang="scss">

    $size: 30px;
    $borderColor: #3F4363;
    $borderHover: #8f94b8a8;
    $active: #2C2F47;
    $transition: 0.3s ease-in-out; 

    .customCheckbox {
        width: $size;
        height: $size;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 2px solid $borderColor;
        border-radius: 8px;
        outline: none;
        transition: border-color $transition, background-color $transition;
        cursor: pointer;

        &:focus {
            border-color: $borderHover;
        }

        &_active {
            border-color: $active;
            background-color: $active;
            &:focus {
                border-color: $active;
            }
        }

        &__wrapper {
            display: inline-block;
            & > input[type='checkbox'] {
            display: none;
            }
        }
    }

    @media (any-hover: hover) {
        .customCheckbox {
            &:hover {
                border-color: $borderHover;
            }

            &_active:hover {
                background-color: $borderHover;
            }
        }
    }
</style>