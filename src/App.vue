<template>
  <div class="wrapper">
    <div class="card_editor">
      <div class="header_card">
        <div class="icons" ref="btns">
          <button
            data-command="bold"
            @click="doCommand"
            class="btn__funcionalidade"
          >
            <i class="fas fa-bold"></i>
          </button>

          <button
            @click="doCommand"
            data-command="italic"
            class="btn__funcionalidade"
          >
            <i class="fas fa-italic"></i>
          </button>

          <button
            @click="doCommand"
            data-command="justifyRight"
            class="btn__funcionalidade"
          >
            <i class="fas fa-align-right"></i>
          </button>
          <button
            class="btn__funcionalidade"
            @click="doCommand"
            data-command="justifyCenter"
          >
            <i class="fas fa-align-justify"></i>
          </button>

          <button
            @click="doCommand"
            data-command="justifyLeft"
            class="btn__funcionalidade"
          >
            <i class="fas fa-align-left"></i>
          </button>

          <button
            @click="doCommand"
            data-command="underline"
            class="btn__funcionalidade"
          >
            <i class="fas fa-underline"></i>
          </button>

          <button
            @click="doCommand"
            class="btn__funcionalidade"
            data-command="hiliteColor"
          >
            <i class="fas fa-marker"></i>
          </button>

          <button
            @click="doCommand"
            data-command="cut"
            class="btn__funcionalidade"
          >
            <i class="fas fa-cut"></i>
          </button>
        </div>
      </div>
      <div class="body_card" contenteditable="true"></div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import * as cmds from "./params";
export default {
  setup() {
    const btns = ref(null);
    let buttons = document.getElementsByClassName("btn__funcionalidade");

    const doCommand = () => {
      for (let btn of buttons) {
        btn.addEventListener("click", () => {
          let cmd = btn.dataset["command"];

          for (let valor of cmds.commands) {
            if (valor.cmd == cmd) {
              document.execCommand(cmd, false, valor.val || null);
            }
          }
        });
      }
    };

    return {
      btns,
      doCommand,
    };
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #edeced;

  .card_editor {
    background: white;
    border-radius: 5px;
    width: 70%;
    height: 80vh;
    padding: 1rem;

    .header_card {
      border-bottom: 1px solid rgb(235, 234, 234);
      height: 15%;

      .icons {
        height: 100%;
        display: flex;
        align-items: center;

        button {
          background: none;
          border: none;
          cursor: pointer;
          margin: 0 0.5rem;

          i {
            transition: 0.1s ease-in-out;

            &:hover {
              color: rgb(94, 94, 94);
            }
          }
        }
      }
    }
    .body_card {
      height: 80%;
      border: 1px solid rgb(238, 237, 237);
      padding: 0.5rem;
      overflow-y: auto;
      &:focus {
        outline: none;
      }
    }
  }
}

@media screen and(max-width:500px) {
  .card_editor {
    width: 90% !important;
  }
}

@media screen and(max-width:700px) {
  .card_editor {
    width: 80% !important;
  }
}
</style>