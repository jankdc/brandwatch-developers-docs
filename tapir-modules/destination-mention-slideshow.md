# destination-mention-slideshow

## Data format
See [schema.json](https://github.com/vizia/destination-mention-slideshow/schema.json) for a json-schema specifying the format of valid input data to this destination.

## Valid Data Example

```json
{
    "author": {
        "primaryName":"Donny Donson",
        "secondaryName":"@donny",
        "avatarSrc":"https://pbs.twimg.com/profile_images/652241511623471104/4-8NeNYm.jpg"
    },
    "contentType":"twitter",
    "date":"2016-03-04T09:32:17.000+0000",
    "mediaUrls":[
        "https://s3.amazonaws.com/lifesite/Miscellaneous/Donny_Osmond.jpg"
    ],
    "snippet":"Pal pal is it you there?",
    "snippetHighlights":[
        "American",
        "Airlines"
    ]
}
```

## Demo

```sh
npm run watch
```

## Config

The following config props can be specified:

- `highlightSnippet` - `Boolean` - if true strings in the `snippetHighlights` prop are highlighted within the rendered snippet.
- `imageFolderPath` - `String | undefined` - optionally specify a folder for images.
