# @vizia/source-google-analytics

## Config

```
{
    scene: {
        options: {
            tokens: {
                google: 'your-google-token'
            },
            viewId: 'your-ga-view',
            metrics: ['ga:uniquePageviews'],
            startDate: '6daysAgo',
            endDate: 'today'
        }
    }
}
```

## Schema

This source returns data in format:

```
{
     metric1: 'totalValue',
     metric2: 'totalValue'
 }
```

e.g. a query for the metrics `ga:uniquePageViews` and `ga:sessions` returns

```
{ 'ga:uniquePageviews': '5649', 'ga:sessions': '1580' }
```

## Demo

```
npm start -- -t <YOUR_GOOGLE_OAUTH_TOKEN> -v <GA view id> [-s start date (6daysAgo)] [-e end date (today)] [-m metric (ga:uniquePageviews)]
```

By default only a token and ga view id are required.

## Getting a token (Internal BW)

Simplest way is to go to your dev instance of [auth service](https://auth.vizia.vizialocal.io) and generate a google token.

## Fetching a fresh token

Google tokens expire within a couple hours. Fortunately the auth service can refresh your token for you. Simply refreshing the demo page will generate a new token for you if you need it.

If you are feeling more adventurous and want to automate this then you need to find your token uuid as follows:

1. `redis-cli -n 11`
2. `hgetall AVAILABLE_AUTHS:coole-bundle:google:6969`

This will spit out a list of all available demo token uuids e.g.:

```
1) "Ollie Edwards"
2) "b225b93e-8438-4631-abdf-0243ab2ef5f7"
```

Make a note of the uuid (2). This uuid remains static even when the token changes. You can now run the following command whenever you like to update the `$GOOGLE_ANALYTICS_TOKEN` env var

```
export GOOGLE_TOKEN=`UUID=<YOUR_UUID> bash -c 'curl -s https://auth.vizia.vizialocal.io/token/$UUID?bwClientId=6969 -H "Authorization: authServiceToken token=super-secret-auth-token" | sed -n "s/.*$UUID\"\:\"\([^\"]*\).*$/\1/p"'`
```
