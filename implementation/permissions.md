# Permissions

This document describes how permissions are defined in the Sportily API project.

### Architecture

To do...

### Defining permissions

#### Individual actions

Each permission rule consists of:

- The name of the action.
- The type of entity being acted upon.
- A callback that decides at run-time whether the permission is granted. It is provided with the entity an which an action is being performed.

For example:

```php
$allow('read', 'Team', function($entity) use($role) {
    return $entity->id == $role->team_id;
});
```

Here, the user is being granted access to retrieve an individual team, but only if the user belongs to that team.

#### Create, read, update, delete

When defining administrator roles, it's helpful to be able to great access to all of the CRUD operations in one go. To support this, a `crud` alias has been setup.

For example:

```php
$allow('read', 'Season', function($entity) use($role) {
    return $entity->organisation_id == $role->organisation_id;
});
```

Here, the user is being granted access to create new seasons, retrieve seasons, update existing seasons, and delete seasons, but only if seasons that belong to an organisation the user is an administrator at.

#### Filtering collections

The `index` action is reserved for listing and filtering collections. When defining rules for this action, the `$allow` function supports two argument types. If the third argument is a function then it is called as normal, with an instance of `FilterQuery` passed in. The `FilterQuery` represents all of the filter arguments passed in the request query string.

For example:

```php
$allow('index', 'Member', function($query) {
    return $query->canUpdate();
});
```

In this example, the `canUpdate` method is called on the `FilterQuery`. This method checks whether the authenticated user has permission to update all the entities identified in the filters. If the request contains the filter `team_id=42` then the user would need permissions to update the team to be allowed to list the members for it.

This can be useful for defining `index` rules for administrators, but in other scenarios it can be cumbersome to check the entire filter set in the permission rules. It is often preferable to define the rules on a per-filter basis, like so:

For example:

```php
$allow('read', 'Member', ['team_id' => function($team_id) use($role) {
    return $team_id == $role->team_id;
}]);
```

Here, the third argument to `$allow` is an associative array, containing a single entry, the key of which is the filter name and the value is the callback. In this scenario, only the value of that filter is passed to the callback.
