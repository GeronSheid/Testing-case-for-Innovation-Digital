<script lang="ts">
    import Button from "./button.svelte";
    export let notificationText: string;
    export let notificationTitle: string;
    export let notificationStatus: boolean;
    export let isVisible: boolean = false;
    export let onClose: () => void;

    const handleContentClick = (event: MouseEvent) => {
        event.stopPropagation();
    }

</script>

{#if isVisible}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div class="notificationCard__overlay" on:click={onClose}>
    <div class="notificationCard" on:click={handleContentClick}>
        <h2>{notificationTitle}</h2>
        {#if notificationStatus}
            <svg width="15" height="11" viewBox="0 0 15 11" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path opacity="0.7" d="M14.5607 0.429557C13.9749 -0.143186 13.0254 -0.143186 12.4396 0.429557L5.24994 7.45867L2.56038 4.82963C1.97536 4.25689 1.02434 4.25689 0.439324 4.82963C-0.146441 5.40237 -0.146441 6.33079 0.439324 6.90353L4.18942 10.5703C4.48193 10.857 4.86593 11 5.24994 11C5.63395 11 6.01796 10.857 6.31047 10.5703L14.5607 2.50346C15.1464 1.93072 15.1464 1.0023 14.5607 0.429557Z" fill="currentColor"/>
            </svg>
        {:else}
            <svg width="15" height="15" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M22.6066 21.3934C22.2161 21.0029 21.5829 21.0029 21.1924 21.3934C20.8019 21.7839 20.8019 22.4171 21.1924 22.8076L22.6066 21.3934ZM40.9914 42.6066C41.3819 42.9971 42.0151 42.9971 42.4056 42.6066C42.7961 42.2161 42.7961 41.5829 42.4056 41.1924L40.9914 42.6066ZM21.1924 41.1924C20.8019 41.5829 20.8019 42.2161 21.1924 42.6066C21.5829 42.9971 22.2161 42.9971 22.6066 42.6066L21.1924 41.1924ZM42.4056 22.8076C42.7961 22.4171 42.7961 21.7839 42.4056 21.3934C42.0151 21.0029 41.3819 21.0029 40.9914 21.3934L42.4056 22.8076ZM21.1924 22.8076L40.9914 42.6066L42.4056 41.1924L22.6066 21.3934L21.1924 22.8076ZM22.6066 42.6066L42.4056 22.8076L40.9914 21.3934L21.1924 41.1924L22.6066 42.6066Z" fill="currentColor"/>
            </svg>
        {/if}
        <p>{notificationText}</p>
        <Button
            type='default'
            onClick={onClose}
        >
        Go back
        </Button>
    </div>
</div>
{/if}

<style lang="scss">
    $background: #171929;
    .notificationCard {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 0.83rem;
        padding: 1.4rem;
        background-color: $background;
        border-radius: 27px;
        font-size: 0.8rem;
        z-index: 15;

        & > svg {
            border: 2px solid #fff;
            padding: 0.83rem;
            border-radius: 50%;
        }

        &__overlay {
            background-color: #0000007e;
            position: fixed;
            inset: 0;
            z-index: 10;
        }
    }
</style>