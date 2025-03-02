## procs

Procs may be derived from /proc. These procs are "global", in
that they can be called anywhere in the code.
### Example:

```dm
proc/poof()
    world << "POOF!"
```
 
The proc `poof()` may now be called anywhere in the code. 

Procs may also be attached to objects by defining them under the appropriate
`object/proc` subnode. Currently DM allows procs to be defined or
overridden for `/mob`, `/obj`, `/turf`, `/area`, `world`, and `/client`,
as well as for [datum objects](/ref/datum.md)  derived from `/`. Predefined
procs are discussed under the "procs" entry for the object type.
### Example:

```dm
mob/proc/poof()
    world << "POOF!"
```

This can be called by a mob var M, using `M.poof()`.
### Return types

It is possible to define what type of value a proc is expected
to return, by following its definition with an `as` clause. This can be
a type path, such as `as /mob/player`, or a more intrinsic type like
`as num` or `as list`.
### Example:

```dm
mob/monster
    var/mob/player/target

    proc/GetTarget() as /mob/player
        if(!target)
            // find a /mob/player in view
            target = locate() in view(src)
        return target
```

Currently the only
purpose for using the `as` clause is for situations where the compiler
needs to infer the type of an expression. Mainly this applies to the
[.](/ref/operator/%2e.md)  and [?.](/ref/operator/%3f%2e.md) operators
in an expression such as `GetTarget()?.Attack(src)`. Giving
`GetTarget()` a return type allows the compiler to check if `Attack()`
is a valid proc for `/mob/player`. Otherwise, the `.` and `?.` operators
act like `:` and `?:`, respectively; the compiler won\'t do any checking
to see if `Attack()` is valid.

> [!TIP] 
> **See also:**
> +   [vars (procs)](/ref/proc/var.md) 
> +   [arguments (proc)](/ref/proc/arguments.md) 
> +   [procs (area)](/ref/area/proc.md) 
> +   [procs (mob)](/ref/mob/proc.md) 
> +   [procs (obj)](/ref/obj/proc.md) 
> +   [procs (turf)](/ref/turf/proc.md) 