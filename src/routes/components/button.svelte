<script lang="ts">
  export let disabled: boolean = false;
  export let onClick: () => void;
  export let type: "default" | "succes" | "attention" | "danger";

  const styleObj = {
    default: "",
    succes: "customBtn_succes",
    attention: "customBtn_attention",
    danger: "customBtn_danger",
  };
</script>

<button
  class={`customBtn ${styleObj[type]}`}
  on:click|preventDefault={onClick}
  {disabled}
>
  <slot></slot>
</button>

<style lang="scss">
  $default: #2c2f47;
  $hover: #404463;
  $succes: #00b945;
  $succesHov: #008d34;
  $attention: #ff7a00;
  $attentionHov: #c55f00;
  $danger: #ff1800;
  $dangerHov: #aa1202;
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
    transition: background-color 0.3s ease-in-out;

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

  @media (any-hover: hover) {
    .customBtn {
      &:hover {
        background-color: $hover;
        &_succes {
          background-color: $succesHov;
        }

        &_atention {
          background-color: $attentionHov;
        }

        &_danger {
          background-color: $dangerHov;
        }
      }
    }
  }

  @media (max-width: 900px) {
    .customBtn {
      width: 100%;
    }
  }
</style>
