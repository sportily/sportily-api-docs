# Stats

## Player Stats

### Top Goal Scorers

Endpoint: `GET /stats/top-scorers`

```js
{
  data: [
    {
      position: 1,
      role_id: 1337,
      name: {
        given_name: 'Joe',
        family_name: 'Bloggs'
      },
      fields: {
        played: 2,
        goals: 4,
        assists: 1,
        penalty_seconds: 0,
        points: 5
      }
    }, {
      /* ... */
    }
  ]
}
```

### Top Goalkeepers

Endpoint: `GET /stats/top-goalkeepers`

```js
{
  data: [
    {
      position: 1,
      role_id: 1337,
      name: {
        given_name: 'Gary',
        family_name: 'Goalkeeper'
      },
      fields: {
        played: 2,
        goals_conceded: 3,
        clean_sheets: 1
      }
    }, {
      /* ... */
    }
  ]
}
```

## Team Stats

### Team Standings

Endpoint: `GET /stats/team-standings`

```js
{
  data: [
    {
      position: 1,
      division_entry_id: 42,
      name: 'Sheffield Steelers',
      fields: {
        played: 2,
        won: 1,
        drawn: 1,
        lost: 0,
        points: 3
      }
    }, {
      /* ... */
    }
  ]
}
```
