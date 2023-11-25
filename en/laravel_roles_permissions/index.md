# Laravel Roles Permissions


**Create role, permission**
```php
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

$role = Role::create(['name' => 'admin']);
$permission = Permission::create(['name' => 'create-articles']);
```

**Assign / Sync / Revoke permission to role**
```php
// Assign
$role->givePermissionTo($permission); // $permission can be string / object / array of strings / array of objects
$permission->assignRole($role);

// Sync
$role->syncPermissions($permissions);
$permission->syncRoles($roles);

// Revoke
$role->revokePermissionTo($permission);
$permission->removeRole($role);

```

**Check roles permissons**
```php
$role->hasPermissionTo($permission);
$role->hasAnyPermission($permissions);
$role->hasAllPermissions($permissions);

```
<!--more-->
**Authenticatable user with roles / permissions**

The model:
```php
use Illuminate\Foundation\Auth\User as Authenticatable;
use Spatie\Permission\Traits\HasRoles;

class User extends Authenticatable
{
    use HasRoles;

    // ...
}
```

**Assign / Sync / Revoke permission / role to user**
```php
// Direct permission
$user->givePermissionTo($permission); // $permission: string / multiple strings / array of strings
$user->revokePermissionTo($permission);
$user->syncPermissions($permissions); // $permissions: Array of permissions name

// Via role
$user->assignRole($roles);
$user->removeRole($roles);
$user->syncRoles($roles);
```

**Check user permissions / roles**
```php
// Permissions
$user->hasPermissionTo($permission);
$user->hasAnyPermission($permissions);
$user->hasAllPermissions($permissions);
$user->can($permission);

// Roles
$user->hasRole($roles);
$user->hasAnyRole($roles);
$user->hasAllRoles($roles);
```

**Get permission / role**
```php
$permissionNames = $user->getPermissionNames();
$permissions = $user->permissions;
$permissions = $user->getDirectPermissions();
$permissions = $user->getPermissionsViaRoles();
$permissions = $user->getAllPermissions();
$roles = $user->getRoleNames();
```

**Model scope**
```php
$users = User::role('admin')->get(); // Will return all users with role admin. role parameter can be: String / Array of strings / Object / Array of objects
$users = User::permission('edit-users')->get(); // Returns only users with the permission 'edit-users' (inherited or directly)
```

**Eloquent**
```php
$all_users_with_all_their_roles = User::with('roles')->get();
$all_users_with_all_direct_permissions = User::with('permissions')->get();
$all_roles_in_database = Role::all()->pluck('name');
$users_without_any_roles = User::doesntHave('roles')->get();
$all_roles_except_a_and_b = Role::whereNotIn('name', ['role A', 'role B'])->get();
```
