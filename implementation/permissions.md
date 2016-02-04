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
