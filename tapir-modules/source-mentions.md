# Mention source

A Tapir-compatible HTTP source for Brandwatch mentions.

### Demo

Ensure `$VIZIA_TOKEN` is set in your environment, then:

```
./cli.js --pageSize=50 --rollingDateRangeValue=7
```

## Usage

```js
source.create({
    scene: {
        options: {
            projectId: 'fakeProjectId',
            filter: {
                queryId: [
                    'fakeQuery1',
                    'fakeQuery2'
                ],
                orderDirection: 'desc',
                otherQueryParam: 'lol'
            },
            startDate: 'startDate',
            endDate: 'endDate',
            rollingDateRangeValueValue: 7 // Instead of startDate and endDate
        }
    },
    bwApiRootUrl: 'fakeApi',
    token: 'fakeToken'
});
```

If no dates (or `rollingDateRangeValueValue`) are provided, it will return the latest mentions according to the `pageSize`. **NB:** This will always force the HTTP requests to use the `orderDirection=desc` parameter. Should the pipeline config use `orderDirection: 'asc'`, the response array will be reversed.
