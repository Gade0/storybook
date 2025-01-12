---
title: 'Sidebar & URLS'
---

Storybook’s sidebar lists all your stories grouped by component. When you have many components, you may also wish to group those components. To do so, you can add the `/` separator to the `title` of your CSF file and Storybook will group the stories into groups based on common prefixes:

![Storybook sidebar anatomy](./sidebar-anatomy.jpg)

We recommend using a nesting scheme that mirrors the filesystem path of the components. For example, if you have a file `components/modals/Alert.js` name the CSF file `components/modals/Alert.stories.js` and title it `Components/Modals/Alert`.

## Roots

By default, Storybook will treat your top-level nodes as “roots”. Roots are displayed in the UI as “sections” of the hierarchy. Lower level groups will show up as folders:

![Storybook sidebar story roots](./sidebar-roots.jpg)

If you’d prefer to show top-level nodes as folders rather than roots, you can set the `sidebar.showRoots` option to `false` in [`./storybook/manager.js`](./overview.md#configure-story-rendering):

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/storybook-manager-disable-roots.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

## Automatically generate titles

With CSF 3.0 files, you can choose to leave out a title and let it be inferred from the story's path on disk instead:

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/component-story-auto-title.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

This is controlled by the way your stories are configured:

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/component-story-configuration.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

Given this configuration, the stories file `../src/components/MyComponent.stories.tsx` will get the title `components/MyComponent`.

You can further customize the generated title by modifying the stories configuration.

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/component-story-configuration-custom.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

This configuration would match a custom file pattern, and add a custom prefix of Foo to each generated title.

## Permalinking to stories

By default, Storybook generates an `id` for each story based on the component title and the story name. This `id` in particular is used in the URL for each story, and that URL can serve as a permalink (primarily when you [publish](../sharing/publish-storybook.md) your Storybook).

Consider the following story:

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/foo-bar-baz-story.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

Storybook's ID-generation logic will give this the `id` `foo-bar--baz`, so the link would be `?path=/story/foo-bar--baz`.

It is possible to manually set the id of a story, which is helpful if you want to rename stories without breaking permalinks. Suppose you want to change the position in the hierarchy to `OtherFoo/Bar` and the story name to `Moo`. Here's how to do that:

<!-- prettier-ignore-start -->

<CodeSnippets
  paths={[
    'common/other-foo-bar-story.js.mdx',
  ]}
/>

<!-- prettier-ignore-end -->

Storybook will prioritize the `id` over the title for ID generation if provided and prioritize the `story.name` over the export key for display.