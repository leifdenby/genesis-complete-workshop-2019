# Using luigi pipelines in the GENESIS toolkit

The GENESIS toolkits functionality is available via luigi pipelines defined in
`genesis.utils.pipeline.data` and `genesis.utils.pipeline.viz` for data
manipulation and production of visualisations (plots) respectively.

To use the analysis pipeline in GENESIS the data sources to be analysed need to
be defined in a YAML-file called `datasources.yaml`. In this directory you can
see that a data source given the "base name" `no_shear.tn6` (representing the
non-sheared simulation you've been provided at time step 6) has been added.

Luigi tasks are started may be started with `luigi --local-scheduler --module
ModuleName`, so to create for example a horizontal cross-section plot of
vertical velocity at z~200m you can simply run the luigi Task called
`CrossSection` defined in `genesis.utils.pipeline.viz` with

```bash
> luigi --local-scheduler --module genesis.utils.pipeline.viz.CrossSection --base-name no_shear.tn6 --var-name w --z 200
```

To simplify running the pipeline tasks you can setup the command prompt aliases
in `genesis-aliases` with

```bash
> source genesis-aliases
```

And then the above command becomes

```bash
> genesis-viz CrossSection --base-name no_shear.tn6 --var-name w --z 200
```

Once the task has run you will notice that `data/` in the current directory has
become populated by the output produced by all the intermediate tasks which
were run.


## Available pipeline tasks for visualisation

All tasks mentioned here a stored in the `genesis.utils.viz` module and each
produce a plot. Some of the available tasks will be listed below, but have
a look in the module for a full list.

### `CumulantScalesProfile`

Creates vertical profile plot of cumulant lenght-scales.

```bash
> genesis-viz CumulantScalesProfile --base-names no_shear.tn6 --cumulants w:d_qv,w:w,qv:qv
```

### `ObjectsScaleDist`

Produce histogram (or probability density with `--as-density` flag) of object
properties for the objects identified

```bash
> genesis-viz ObjectsScaleDist --base-names no_shear.tn6 --mask-method rad_tracer_thermals --mask-method-extra-args num_std_div=2.0 --object-splitting-scalar w --var-name r_equiv
```

For this task you can also provide filters to look only at the objects with
a given property. For example to look only at objects which extend above z=500m
the above command becomes

```bash
> genesis-viz ObjectsScaleDist --base-names no_shear.tn6 --mask-method rad_tracer_thermals --mask-method-extra-args num_std_div=2.0 --object-splitting-scalar w --var-name r_equiv --object-filters prop:z_max__gt=500
```

### `ObjectsScalesJointDist`

As `ObjectsScaleDist` but joint distributions for two object properties defined
through arguments `--x` and `--y` for the variables to be plotted along the x-
and y-axis.

```bash
> genesis-viz ObjectsScalesJointDist --base-names no_shear.tn6 --mask-method rad_tracer_thermals --mask-method-extra-args num_std_div=2.0 --object-splitting-scalar w --x r_equiv --y z_max
```

As above you can pass in object filters to this command. For example to only
view objects which have a maximum vertical velocity (per-object)

```bash
> genesis-viz ObjectsScalesJointDist --base-names no_shear.tn6 --mask-method rad_tracer_thermals --mask-method-extra-args num_std_div=2.0 --object-splitting-scalar w --x r_equiv --y z_max --object-filters prop:w__maximum__gt=1.0
```

### `ObjectScaleVsHeightComposition`

Create decomposition plot where values of scalar field (for example water
vapour vertical flux `qv_flux`) as decomposed by an object property (for
example equivalent spherical radius `r_equiv`)

```bash
genesis-viz ObjectScaleVsHeightComposition --base-name no_shear.tn6 --object-splitting-scalar w --mask-method rad_tracer_thermals --mask-method-extra-args num_std_div=2.0 --field-name qv_flux --x r_equiv --z-max 600. --dx 50. --x-max 800.
```

As the other object-based methods above you may provide object-filters to this
through `--object-filters`.
