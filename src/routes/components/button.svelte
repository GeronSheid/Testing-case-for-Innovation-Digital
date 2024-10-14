<script lang="ts">
    export let disabled: boolean = false;
    export let onClick: () => void;
    export let type: 'default' | 'succes' | 'attention' | 'danger';

    const styleObj = {
        default: '',
        succes: 'customBtn_succes',
        attention: 'customBtn_attention',
        danger: 'customBtn_danger'
    }

</script>

<button
    class={`customBtn ${styleObj[type]}`}
    on:click|preventDefault={onClick}
    disabled={disabled}
>
    <slot></slot>
</button>

<style lang="scss">

    $default: #2C2F47;
    $succes: #00B945;
    $attention: #FF7A00;
    $danger: #FF1800;
    $shadow: 0 0 50px #000000bb;
    $textMain: #fff;

    .customBtn {
        min-height: 22px;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 40px;
        color: $textMain;
        background-color: $default;
        border: none;
        outline: none;
        border-radius: 50px;
        box-shadow: $shadow;
        cursor: pointer;

        &_succes {
            background-color: $succes;
        }

        &_atention {
            background-color: $attention;
        }

        &_danger {
            background-color: $danger;
        }
    }

    @media (max-width: 900px) {
        .customBtn {
            width: 100%;
        }
    }
</style>