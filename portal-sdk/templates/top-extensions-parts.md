# Parts

## Overview

Parts, also known as Tiles, are the units of UI that can participate on Azure dashboards. This includes the procedures used to create parts.

* [Creating a basic part](#creating-a-basic-part)

* [Pinning a part manually](#pinning-a-part-manually) 

* [Pinning a part programmatically](#pinning-a-part-programmatically) 

* [Offering a part in the Tile gallery](#offering-a-part-in-the-tile-gallery)

### Creating a basic part

**NOTE**: In this discussion, `<dir>` is the `SamplesExtension\Extension\` directory, and  `<dirParent>`  is the `SamplesExtension\` directory, based on where the samples were installed when the developer set up the SDK. 

Creating a part is very similar to creating a blade. And like blades, there are important decisions to be made while planning to implement the part.  The recommended way is to implement a template part.  Template parts are like template blades. You define an html template and bind it to a TypeScript view model, as in the following example.

```
{"gitdown": "include-file", "file":"../Samples/SamplesExtension/Extension/Client/V2/Parts/TemplatePart/SimpleTemplatePart.ts"}
```

**NOTE**: The context property on the part view model contains useful APIs on it for things like opening blades, putting the part into an error state, and more.

If you need more control over the DOM and are willing to take on additional burdens regarding accessibility and theming then you can also choose to build a `FramePart` where the contents of the part are implemented by using an iFrame that you can control. The following  example demonstrates  a simple FramePart that shows how to communicate between the visible iFrame and the hidden extension iFrame.

```
{"gitdown": "include-file", "file":"../Samples/SamplesExtension/Extension/Client/V2/Parts/FramePart/SampleFramePart.ts"}
```

### Pinning a part manually

This is for when a user clicks on the pin icon on a blade.

If you have built a blade and have added the `@TemplateBlade.Pinnable.Decorator()` decorator that is available for TemplateBlade and all the other Blade variants, then the compiler will require you to implement an `onPin()` function. This function is called by the framework when the user manually clicks the blade's pin icon.  The extension returns a `PartReference` in that function. When the  extension is built, a PartReference class will be autogenerated for each part defined in the extension. 

To access the part references from within a blade, the extension imports the following reference.

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/Pinning/PinnableBlade.ts", "section": "top-extensions-parts#pinning-import"}

Then in the `onPin()` function you can do something like this:

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/Pinning/PinnableBlade.ts", "section": "top-extensions-parts#pinning-on-pin"}

This enables the extension to initialize the part, as in the following example.

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/Pinning/PinnableBlade.ts", "section": "top-extensions-parts#pinning-get-reference"}

### Pinning a part programmatically 

You can programmatically pin a part to the current dashboard when a user is interacting with one of your blades. To do this, first import the PartPinner module like this.

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/Pinning/PinnableBlade.ts", "section": "top-extensions-parts#pinning-import2"}

Then from within your code you can imperatively call the `pin()` function, as in the following code.

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Blades/Pinning/PinnableBlade.ts", "section": "top-extensions-parts#pinning-on-pin-from-ui-click"}

### Offering a part in the Tile gallery

The Tile Gallery is presented when users create new dashboards or when they put their dashboard in edit mode. The Gallery lets users browse and search through all parts built by all extensions, as long as the parts have the right metadata. If you want your part to be included in the tile gallery then you just need to provide a little bit of metadata inside of your part's decorator. 

The following example includes the `galleryMetadata` property that lets the developer specify a localized title and category, in addition to a thumbnail image. 

{"gitdown": "include-section", "file":"../Samples/SamplesExtension/Extension/Client/V2/Parts/PartGallery/GeneralGalleryPart.ts", "section": "top-extensions-parts#template-decorator"}

 {"gitdown": "include-file", "file": "../templates/portalfx-extensions-bp-parts.md"}

 {"gitdown": "include-file", "file": "../templates/portalfx-extensions-faq-parts.md"}

 {"gitdown": "include-file", "file": "../templates/portalfx-extensions-glossary-parts.md"}