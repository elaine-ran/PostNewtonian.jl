# Dynamics

## Integrating orbital evolution

```@docs
orbital_evolution
uniform_in_phase
estimated_time_to_merger
fISCO
ΩISCO
```

## Detecting the up-down instability

```@autodocs
Modules = [PostNewtonian]
Pages   = ["dynamics/up_down_instability.jl"]
Order   = [:module, :type, :constant, :function, :macro]
```

## Approximants

These compute the right-hand sides for the ODE integration of PN orbital
evolutions.  They only differ in how they compute the time dependence of the
fundamental PN variable ``v``.  Fundamentally, we have
```math
\frac{dv}{dt} = -\frac{\mathcal{F} + \dot{M}_1 + \dot{M}_2} {\mathcal{E}'}
```
as the essential expression.  The various approximants differ simply in how they
expand this expression.

Note that `TaylorT2` and `TaylorT3` can also be [found in the
literature](https://arxiv.org/abs/0710.0158), and are used to derive analytical
expressions for the orbital evolution.[^2]  Unfortunately, this can only be
accomplished for non-precessing systems, so we don't bother to implement them in
this package.

[^2]: The second `T` in the `TaylorTn` names refers to the fact that these
    calculations provide the dynamics in the *time* domain.  In a manner
    following `TaylorT2`, it is also possible to use the stationary-phase
    approximation to derive the dynamics in the *frequency* domain, thus
    resulting in [the `TaylorF2` approximant](https://arxiv.org/abs/0901.1628).
    Finally, it should be noted that approximants named `TaylorK1`, `TaylorK2`,
    and `TaylorEt` [have also been introduced](https://arxiv.org/abs/0712.3236).
    None of these other approximants have been implemented in this package.

```@autodocs
Modules = [PostNewtonian]
Pages   = ["dynamics/right_hand_sides.jl"]
Order   = [:module, :type, :constant, :function, :macro]
```


Note that, internally, the `TaylorT*` functions call `causes_domain_error!`.  This is a fairly simplistic detection of when evolved parameters will lead to bad values.  It may be
desirable to extend this detection to be more sophisticated.
```@docs
PostNewtonian.causes_domain_error!
```
