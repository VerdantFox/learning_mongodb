# Examples

## Search for text matches exact
{"Title": "Titanic"}

## Search for range
{"Created": {$gte: 1990, $lt: 2005}}

## Search on inner field
{"awards.oscars.bestAnimatedFeature": "won"}

## And queries
{"awards.wins": 2, "awards.nominations": 2}

## Equality matches on arrays (entire array must match)
{"cast": ["Jeff Bridges", "tim Robbins"]}

## Equaltiy matches on arrays (one item must match)
{"cast": "Jeff Bridges"}

## Equaltiy matches on arrays (item at index 0)
{"cast.0": "Jeff Bridges"}

# Resources

## query operators
docs.mongodb.com/manual/reference/operator/query/


