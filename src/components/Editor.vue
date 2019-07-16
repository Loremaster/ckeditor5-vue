<template>
  <div class="editor">
    <ckeditor
      :editor="editor"
      v-model="editorData"
      :config="editorConfig"
      @input="onEditorInput"
    />
  </div>
</template>

<script>
import ClassicEditor from "@ckeditor/ckeditor5-editor-classic/src/classiceditor";
import EssentialsPlugin from "@ckeditor/ckeditor5-essentials/src/essentials";
import BoldPlugin from "@ckeditor/ckeditor5-basic-styles/src/bold";
import ItalicPlugin from "@ckeditor/ckeditor5-basic-styles/src/italic";
import LinkPlugin from "@ckeditor/ckeditor5-link/src/link";
import ParagraphPlugin from "@ckeditor/ckeditor5-paragraph/src/paragraph";
import Font from "@ckeditor/ckeditor5-font/src/font";
import PasteFromOffice from "@ckeditor/ckeditor5-paste-from-office/src/pastefromoffice";

export default {
  name: "Editor",
  data() {
    return {
      editor: ClassicEditor,
      editorData: "<p>Content of the editor.</p>",
      editorConfig: {
        plugins: [
          EssentialsPlugin,
          PasteFromOffice,
          BoldPlugin,
          ItalicPlugin,
          LinkPlugin,
          ParagraphPlugin,
          Font
        ],
        fontFamily: {
          options: [
            "Arial, Helvetica, sans-serif",
            "Ubuntu, Arial, sans-serif",
            "Ubuntu Mono, Courier New, Courier, monospace"
          ]
        },
        toolbar: {
          items: [
            "bold",
            "italic",
            "link",
            "undo",
            "redo",
            "fontSize",
            "fontFamily",
            "fontColor",
            "fontBackgroundColor"
          ]
        }
      }
    };
  },
  methods: {
    onEditorInput(text, event, editor) {
      const root = event.source.getRoot();

      editor.model.change(writer => {
        //// const position = editor.model.document.selection.getFirstPosition()
        writer.setSelection(root, "in");
        editor.execute("fontFamily", { value: "Arial" });
        writer.setSelection(null);
      });
    }
  }
};
</script>
