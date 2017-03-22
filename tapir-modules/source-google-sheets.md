# @vizia/source-google-sheets

This is your spreadsheets on Vizia.

## Config

```
{
    scene: {
        options: {
            tokens: {
                google: 'your-google-token'
            },
            sheetId: 'your-spreadsheet-id',
            range: '[Sheet1] your-range'
        }
    }
}
```

## Schema

This source returns an instance of google sheets [ValueRange](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets.values#ValueRange)

## Demo

```
npm start -- -t <YOUR_GOOGLE_OAUTH_TOKEN> [-r custom range] [-s sheet id]
```

By default only a token is required and the sheet and range will default to [a dummy testing sheet](https://docs.google.com/spreadsheets/d/1wx7uUAoHTklrl7uWWmjBBZHz2-OhEHsWXGHAeW2-5t0/edit#gid=0) and "Sheet1"

See [api docs](https://developers.google.com/sheets/api/guides/concepts) for info on range syntax.

## Getting a token (Internal BW)

Simplest way is to go to your dev instance of [auth service](https://auth.vizia.vizialocal.io) and generate a google token.
