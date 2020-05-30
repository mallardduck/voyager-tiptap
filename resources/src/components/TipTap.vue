<template>
    <div class="tiptap">
        <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
            <div class="button-group">
                <button class="button font-bold small icon-only" :class="[isActive.bold() ? 'dark-gray' : 'accent']" @click="commands.bold" v-tooltip="__('voyager::wysiwyg.bold')">
                    B
                </button>
                <button class="button italic small icon-only" :class="[isActive.italic() ? 'dark-gray' : 'accent']" @click="commands.italic" v-tooltip="__('voyager::wysiwyg.italic')">
                    I
                </button>
                <button class="button line-through small icon-only" :class="[isActive.strike() ? 'dark-gray' : 'accent']" @click="commands.strike" v-tooltip="__('voyager::wysiwyg.strike')">
                    S
                </button>
                <button class="button underline small icon-only" :class="[isActive.underline() ? 'dark-gray' : 'accent']" @click="commands.underline" v-tooltip="__('voyager::wysiwyg.underline')">
                    U
                </button>
                <div class="divider"></div>
                <button class="button small icon-only" :class="[isActive.code() ? 'dark-gray' : 'accent']" @click="commands.code" v-tooltip="__('voyager::wysiwyg.code')">
                    <icon icon="code" :size="6"></icon>
                </button>
                <button class="button small icon-only" :class="[isActive.paragraph() ? 'dark-gray' : 'accent']" @click="commands.paragraph" v-tooltip="__('voyager::wysiwyg.paragraph')">
                    P
                </button>
                <button class="button small icon-only" :class="[isActive.bullet_list() ? 'dark-gray' : 'accent']" @click="commands.bullet_list" v-tooltip="__('voyager::wysiwyg.bullet_list')">
                    UL
                </button>
                <button class="button small icon-only" :class="[isActive.ordered_list() ? 'dark-gray' : 'accent']" @click="commands.ordered_list" v-tooltip="__('voyager::wysiwyg.ordered_list')">
                    OL
                </button>
                <button class="button small icon-only" :class="[isActive.horizontal_rule() ? 'dark-gray' : 'accent']" @click="commands.horizontal_rule" v-tooltip="__('voyager::wysiwyg.horizontal_rule')">
                    HR
                </button>
                <div class="divider"></div>
                <button class="button small icon-only" :class="[isActive.heading({ level: 1 }) ? 'dark-gray' : 'accent']" @click="commands.heading({ level: 1 })" v-tooltip="__('voyager::wysiwyg.heading_1')">
                    H1
                </button>
                <button class="button small icon-only" :class="[isActive.heading({ level: 2 }) ? 'dark-gray' : 'accent']" @click="commands.heading({ level: 2 })" v-tooltip="__('voyager::wysiwyg.heading_2')">
                    H2
                </button>
                <button class="button small icon-only" :class="[isActive.heading({ level: 3 }) ? 'dark-gray' : 'accent']" @click="commands.heading({ level: 3 })" v-tooltip="__('voyager::wysiwyg.heading_3')">
                    H3
                </button>
                <div class="divider"></div>
                <button class="button small icon-only accent" @click="commands.undo" v-tooltip="__('voyager::wysiwyg.undo')">
                    <icon icon="arrow-left" mirrored :size="6"></icon>
                </button>
                <button class="button small icon-only accent" @click="commands.redo" v-tooltip="__('voyager::wysiwyg.redo')">
                    <icon icon="arrow-right" :size="6"></icon>
                </button>
            </div>
        </editor-menu-bar>

        <editor-content class="content voyager-input" spellcheck="false" :editor="editor" />
    </div>
</template>
<script>
// https://github.com/scrumpy/tiptap
import { Editor, EditorContent, EditorMenuBar } from "tiptap";
import {
    HardBreak,
    Heading,
    HorizontalRule,
    OrderedList,
    BulletList,
    ListItem,
    TodoItem,
    TodoList,
    Bold,
    Code,
    Italic,
    Strike,
    Underline,
    History
} from "tiptap-extensions";

export default {
    props: ['value'],
    components: {
        EditorContent,
        EditorMenuBar
    },
    data: function() {
        return {
            editor: new Editor({
                extensions: [
                    new BulletList(),
                    new HardBreak(),
                    new Heading({ levels: [1, 2, 3] }),
                    new HorizontalRule(),
                    new ListItem(),
                    new OrderedList(),
                    new TodoItem(),
                    new TodoList(),
                    new Bold(),
                    new Code(),
                    new Italic(),
                    new Strike(),
                    new Underline(),
                    new History()
                ],
                content: '',
            })
        };
    },
    methods: {

    },
    computed: {

    },
    beforeDestroy: function () {
        this.editor.destroy();
    }
};
</script>

<style lang="scss" scoped>
.tiptap {
    
    .content {
        @apply min-h-64;
    }
}
</style>

<style lang="scss">
.ProseMirror {
    @apply h-full w-full;
    &:focus {
        outline: none !important;
    }
}
</style>