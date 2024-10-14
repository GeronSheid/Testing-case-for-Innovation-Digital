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
    .customBtn {
        min-height: 22px;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 40px;
        color: #fff;
        background-color: #2C2F47;
        border: none;
        outline: none;
        border-radius: 50px;

        &_succes {
            background-color: #00B945;
        }

        &_atention {
            background-color: #FF7A00;
        }

        &_danger {
            background-color: #FF1800;
        }
    }
</style>