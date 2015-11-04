# Dynamic Fixtures

In Sportily, `fixture_entry` instances are permitted to have `null` as the value of `division_entry_id`. Such fixture entries are considered _dynamic_, and they depend on the results of other events occurring in the system. Dynamic fixtures must have a `rules` value: a JSON structure that describes the fixture. Only when the trigger event occurs will the rules of a dynamic fixture be evaluated and the `division_entry_id` value be populated as a result.

## Supported rules

This section covers the different dynamic fixture rules that are supported, including details of the trigger events that will case the rules to be evaluated.

### Winner of another fixture

The fixture entry will be one of two possible entries, dependant upon which entry wins some other fixture, identified in the example below as `<fixture-id>`. This rule is useful during a knockout stage of a tournament, when the winner of each fixture proceeds through to the next round.

```
{
  "winner_of": <fixture-id>
}
```

### Loser of another fixture

```
{
  "loser_of": <fixture-id>
}
```

### Position in another division

```
{
  "division_position": {
    "division_id": <division_id>,
    "position": <position>
  }
}
```
