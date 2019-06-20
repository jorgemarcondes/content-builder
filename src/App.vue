<template>
  <div>
    <div id="app"></div>
  </div>
</template>

<script>
/* eslint-disable no-console */
// import { schema } from "prosemirror-schema-basic";
import { EditorState } from "prosemirror-state";
import { EditorView } from "prosemirror-view";

import { baseKeymap } from "prosemirror-commands";
import { undo, redo, history } from "prosemirror-history";
import { keymap } from "prosemirror-keymap";
import { Schema,  } from "prosemirror-model";

export default {
  name: "app",
  data() {
    return {};
  },
  mounted() {
    // const schema = new Schema({
    //   nodes: {
    //     doc: { content: "block+" },
    //     paragraph: { group: "block", content: "text*", marks: "_" },
    //     heading: { group: "block", content: "text*", marks: "" },
    //     text: { inline: true }
    //   },
    //   marks: {
    //     strong: {},
    //     em: {}
    //   }
    // });
    const schema = new Schema({
      nodes: {
        doc: { content: "paragraph+" },
        paragraph: {
          content: "text*",
          toDOM(node) {
            return ["p", 0];
          }
        },
        text: {}
      }
    });
    const state = EditorState.create({
      schema,
      plugins: [
        history(),
        keymap({ "Mod-z": undo, "Mod-y": redo }),
        keymap(baseKeymap)
      ]
    });
    // eslint-disable-next-line no-unused-vars
    const view = new EditorView(document.getElementById("app"), {
      state
    });
  }
};
</script>

<style></style>
