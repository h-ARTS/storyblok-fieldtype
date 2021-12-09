<template>
  <div>
    <textarea v-model="model.content" id="mytextarea"></textarea>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  methods: {
    initWith() {
      return {
        plugin: "wysiwyg-tinymce5",
        content: ""
      };
    },
    pluginCreated() {
      this.$sb.getScript(
        "https://cdn.tiny.cloud/1/1dfx5sqlnqa2kcgpekbzff2tmwkf5dvtdo5lva61r7j74svx/tinymce/5/tinymce.min.js",
        () => {
          tinymce.init({
            selector: "#mytextarea",
            menubar: "edit",
            init_instance_callback: editor => {
              editor.on("input change undo redo setcontent", () => {
                this.model.content = editor.getContent();
              });
            },
            height: 350,
            plugins: "fullscreen link lists code visualblocks",
            toolbar:
              "styleselect | fontsizeselect | link | numlist bullist | removeformat",
            content_style:
              ".text-left { text-align: left; } " +
              ".text-center { text-align: center; } " +
              ".text-right { text-align: right; } ",
            fontsize_formats: "14px 15px 16px 17px 18px 20px 24px",
            formats: {
              heading_1: {
                selector: "p, h1, h2, h3, h4, h5, h6",
                classes: "heading--1"
              },
              heading_2: {
                selector: "p, h1, h2, h3, h4, h5, h6",
                classes: "heading--2"
              },
              heading_3: {
                selector: "p, h1, h2, h3, h4, h5, h6",
                classes: "heading--3"
              },
              heading_4: {
                selector: "p, h1, h2, h3, h4, h5, h6",
                classes: "heading--4"
              },
              alignleft: {
                selector: "p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img",
                classes: "text-left"
              },
              aligncenter: {
                selector: "p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img",
                classes: "text-center"
              },
              alignright: {
                selector: "p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img",
                classes: "text-right"
              }
            },
            style_formats: [
              {
                title: "Block",
                items: [
                  {
                    title: "Paragraph",
                    format: "p"
                  },
                  {
                    title: "H1",
                    format: "h1",
                    classes: "heading"
                  },
                  {
                    title: "H2",
                    format: "h2",
                    classes: "heading"
                  },
                  {
                    title: "H3",
                    format: "h3",
                    classes: "heading"
                  },
                  {
                    title: "H4",
                    format: "h4",
                    classes: "heading"
                  },
                  {
                    title: "H5",
                    format: "h5",
                    classes: "heading"
                  },
                  {
                    title: "H6",
                    format: "h6",
                    classes: "heading"
                  },
                  {
                    title: "Blockquote",
                    format: "blockquote"
                  }
                ]
              },
              {
                title: "Inline",
                items: [
                  {
                    title: "Bold",
                    icon: "bold",
                    format: "bold"
                  },
                  {
                    title: "Italic",
                    icon: "italic",
                    format: "italic"
                  },
                  {
                    title: "Underline",
                    icon: "underline",
                    format: "underline"
                  },
                  {
                    title: "Strikethrough",
                    icon: "strike-through",
                    format: "strikethrough"
                  },
                  {
                    title: "Superscript",
                    icon: "superscript",
                    format: "superscript"
                  },
                  {
                    title: "Subscript",
                    icon: "subscript",
                    format: "subscript"
                  },
                  { title: "Code", icon: "sourcecode", format: "code" }
                ]
              },
              {
                title: "Alignment",
                items: [
                  {
                    title: "Text Right",
                    icon: "align-right",
                    format: "alignright"
                  },
                  {
                    title: "Text Center",
                    icon: "align-center",
                    format: "aligncenter"
                  },
                  {
                    title: "Text Left",
                    icon: "align-left",
                    format: "alignleft"
                  }
                ]
              },
              {
                title: "Link Colors",
                items: [
                  {
                    title: "Digi Green",
                    selector: "a",
                    classes: "link--secondary"
                  },
                  {
                    title: "White",
                    selector: "a",
                    classes: "link--secondary-white"
                  }
                ]
              },
              {
                title: "Heading Classes",
                items: [
                  {
                    title: "Heading 1",
                    format: "heading_1"
                  },
                  {
                    title: "Heading 2",
                    format: "heading_2"
                  },
                  {
                    title: "Heading 3",
                    format: "heading_3"
                  },
                  {
                    title: "Heading 4",
                    format: "heading_4"
                  }
                ]
              }
            ]
          });
        }
      );
    }
  },
  watch: {
    model: {
      handler: function(value) {
        this.$emit("changed-model", value);
      },
      deep: true
    }
  }
};
</script>

<style lang="scss">
.mce-tinymce {
  box-sizing: border-box;
}

.p-metatags__google-title {
  color: blue;
  text-decoration: underline;
}

.p-metatags__google-link {
  color: green;
}

.p-metatags__preview {
  margin: 5px 0 15px;
  padding: 10px;
  color: #000;
  background: #fff;
}
</style>
