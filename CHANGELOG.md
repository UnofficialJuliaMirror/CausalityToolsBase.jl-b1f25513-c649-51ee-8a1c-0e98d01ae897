
# Release v0.3.0

## New functionality

- Do custom state space reconstructions with `customembed(pts, positions::Positions, lags::Lags)`. This function acts almost as `DynamicalSystems.reconstruct`, but allows for more flexibility in the ordering of dynamical variables and allows for negative lags. The `positions` variable indicates which dynamical variables are mapped to which variables in the final reconstruction, while `lags` indicates the lags for each of the embedding variables. Example: `customembed([rand(3) for i = 1:50], Positions(1, 2, 1, 3), Lags(0, 0, 1, -2)` gives a 4-dimensional embedding with state vectors `(x1(t), x2(t), x1(t + 1), x3(t - 2))`. Note: `customembed` expects an array of *states*. To embed a vector of time series, load `DynamicalSystems` and wrap the time series in a `Dataset` first, e.g. if `x = rand(100); y = rand(100)` are two time series, then `customembed(Dataset(x, y), Positions(1, 2, 2), Lags(0, 0, 1)` will create the embedding with state vectors `(x(t), y(t), y(t + 1))`. Pre-embedded points may be wrapped in a `CustomReconstruction` instance by simply calling `customembed(preembedded_pts)`.

# Release v0.2.0

A lightweight package providing functionality used throughout the `CausalityTools` ecosystem. 

# New functionality

## New functionality
- **Rectangular binnings**. 
    1. Bin-encode data points relative to some reference point, assuming a rectangular grid. Use `encode` for this.
    2. Determine joint and marginal bin visits given a set of points and a rectangular grid specification. Use `marginal_visits` and `joint_visits` for this.
    3. Compute the unordered histogram (visitation frequency) given a set of points and a rectangular grid specification. Extends `ChaosTools.non0hist` for custom rectangular grids (only cubes are allowed in `ChaosTools`). Can be used with the same  syntax as `marginal_visits`, 
    so that `non0hist(points, ϵ, dims)` will give the histogram over the visited bins of the rectangular grid specified by `ϵ`, considering the marginal
    along the given dimensions (`dims`).  

## Improvements
- Improved documentation for existing methods.

# Release v0.1.0

A lightweight package providing functionality used throughout the `CausalityTools` ecosystem. 

# New functionality
- Wrappers for embedding dimension and lags from `DelayEmbeddings`.
- Abstract partition types. 
- Abstract simplex intersection types. 