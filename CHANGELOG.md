## master

* Add `From<&AsRef<[u8]>> for SharedBytes`.
* Optimise `gpu_cache` hashing to improve benchmark performance by ~30%.

## 0.6.1

* Optimise rasterizer removing internal hashing. Improves draw benchmark
  performance by 11-91%.

## 0.6.0

* Rework gpu_cache data structures allowing constant time hash lookup
  of matching cached glyph textures. Improve performance by ~60-200%.
* Deprecate `gpu_cache::Cache::new` in favour of `gpu_cache::CacheBuilder`.
* Deprecate `gpu_cache::Cache::set_scale_tolerance` &
  `gpu_cache::Cache::set_position_tolerance`. These are now equivalent to
  recreating the cache as they invalidate the cache keys.
* gpu_cache `scale_tolerance` & `position_tolerance` now have subtly different
  meanings but guarantee their error in all cases, where previously the
  worst case was double the set tolerance.

## 0.5.2

* Add gpu cache glyph padding option to fix texture bleeding from other
  glyphs when using interpolated texture coordinates near edges. Use
  `CacheBuilder` to construct a `Cache` that makes use of padding.
* Inlining performance improvements.

## 0.5.1

* Fix tree removal on row clear (gpu_cache).

## 0.5.0

* Let functions like `Font::glyph` and `Font::pair_kerning` work with both
  characters and glyph ids by having them accept any type that implements the
  new `IntoGlyphId` trait. This replaces the `CodepointOrGlyph` enum, which
  didn't seem widely used.
* Make `Font::glyph` always return a `Glyph`, not `Option<Glyph>`. Passing a
  `char` the font doesn't cover returns a `.notdef` glyph (id 0), as it did
  before. Passing an invalid glyph id now panics, like a bad array index: glyph
  ids should only be used to index the font they were looked up for.
* Introduce `rusttype::Error`, which implements `std::error::Error`, `Debug` and
  `Display`, and can be converted to `std::io::Error`.
* Use `Result<_, rusttype::Error>` to report failures in FontCollection, Font
  and associated iterators.
* Add `Font::from_bytes` method similar to `FontCollection::from_bytes` for 1
  font collections.
* Improve gpu_cache performance ~2-6%

## 0.4.3

* Improve gpu_cache performance ~6-17%

## 0.4.2

* Allow users to get font names from `Font`. (#86)

## 0.4.0

* Add more debugging features
* Add support for unscaled fonts
* Improve performance
* Make gpu_cache optional

## 0.3.0

* Transfer to redox-os organization, merge a number of pull requests

## 0.2.1

* Made the API more convenient (courtesy of @mitchmindtree, @I1048576).
* Fixes for the examples (@I1048576)
* Removed the dependency on ndarray (@I1048576)

## 0.2.0

* Initial GPU caching implementation.
* Made font data management more flexible.
* Made the interface for font scales simpler.

## 0.1.2

Fixed issue #8

## 0.1.1

Fixed issue #7

## 0.1

Initial release
