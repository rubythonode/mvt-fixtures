# evilmvt

A require-able suite of valid & invalid vector tile fixtures for testing Mapbox Vector Tile decoding. Located in `fixtures` and [`require()`able](#require-fixtures).

# Fixture suite

The fixtures below are include in `/fixtures`. They are named to be as descriptive as possible, but the table below gives us more space to describe the underlying data.

These are considered "invalid" according to the [Mapbox Vector Tile Specification version 2.1](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto).

Fixture name | Description
---|---
`invalid-Feature-missing-GeomType.mvt` | The `Feature` message is missing a [`GeomType`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L41) message.
`invalid-Feature-multiple-geometries.mvt` | The `Feature` message as multiple [`geometry`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L46) fields encoded, when there should only be one.
`invalid-Feature-no-geometry.mvt` | The `Feature` message has no [`geometry`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L46).
`invalid-Feature-odd_number_tags.mvt` | Only has a single [`tag`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L38) where multiples of 2 are required.
`invalid-Feature-unknown_field_type.mvt` | Has a field value of `10`, which is [not listed as an enum](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L8-L13) and therefore invalid.
`invalid-GeomType-invalid-type.mvt` | The tag for GeomType is `10`, which is invalid.
`invalid-Key-mistyped_uint32.mvt` | Has a [`key`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L63) property incorrectly encoded as a type `std::uint32_t`. | n/a 
`invalid-Layer-extent-mistyped_string.mvt` | Layer [`extent`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L70) is incorrectly encoded as a type `std::string`.
`invalid-Layer-extent-none.mvt` | Missing the [`extent`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L70) type
`invalid-Layer-name-duplicates.mvt` | Includes two layer [`name`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L57)s with the same value: "layer_name".
`invalid-Layer-name-mistyped_uint32.mvt` | Has a layer name incorrectly encoded as `std::uint32_t`.
`invalid-Layer-name-none.mvt` | Does not include a layer name.
`invalid-Layer-name-none-version1.mvt` | Same as above, but version 1 tile.
`invalid-Layer-no-features.mvt` | Layer has no repeated [`Features`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L60) tags.
`invalid-Layer-unknow_value_type.mvt` | Includes a Layer value tag of `20`, which is not defined in the spec.
`invalid-Layer-invalid-version.mvt` | Layer version is `99`, which is invalid according to the specification.
`invalid-Layer-version-mistyped_string.mvt` | Layer version is incorrectly typed as a `std::string`.
`invalid-Layer-version-none.mvt` | Layer does not have a [`version`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L55) property.
`invalid-Tags-nonexistant-values.mvt` | Feature has [`tags`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L38) that point to non-existent [`Keys`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L63) and [`Values`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L66) in the layer.
`invalid-Tile-unknown-tag.mvt` | Tile message has an unknown tag value. The only accepted tag value here is `3`, but this tile encodes a `Feature` with the tag value of `10`.
`invalid-Value-no-fields.mvt` | includes a [`Value`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L66) without any fields encoded within it.
`invalid-Value-multiple-fields.mvt` | The [`Value`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L66) message has two entries, both strings, where there should only be one.
`invalid-Value-string-mistyped_int64.mvt` | A Layer value property is listed as "string" but encoded as `std::int64_t`.
`invalid-Value-unknown-field-type.mvt` | The [`Value`](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L66) has a field with an [unknown type](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L17-L28).
`valid-GeomType-single-linestring.mvt` | Single layer with a valid [linestring geometry](https://github.com/mapbox/vector-tile-spec/tree/master/2.1#4353-example-linestring) from the spec docs.
`valid-GeomType-single-multilinestring.mvt` | Single layer with a valid [multilinestring geometry](https://github.com/mapbox/vector-tile-spec/tree/master/2.1#4354-example-multi-linestring) from the spec docs.
`valid-GeomType-single-multipoint.mvt` | Single layer with a valid [multipoint geometry](https://github.com/mapbox/vector-tile-spec/tree/master/2.1#4352-example-multi-point) from the spec docs.
`valid-GeomType-single-point.mvt` | Single layer with a valid [point geometry](https://github.com/mapbox/vector-tile-spec/tree/master/2.1#4351-example-point) from the spec docs.
`valid-GeomType-single-polygon.mvt` | Single layer with a valid [polygon geometry](https://github.com/mapbox/vector-tile-spec/tree/master/2.1#4355-example-polygon) from the spec docs.
`valid-GeomType-unknown.mvt` | Single geometry with [`UNKNOWN` type](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L9). This is considered "valid" in the lens of the specification. Encoders/decoders can choose to use or throw on this goemetry type.
`valid-Values-all.mvt` | A buffer with all possible [`Value` types](https://github.com/mapbox/vector-tile-spec/blob/master/2.1/vector_tile.proto#L17-L28) encoded in the layer and single Feature.

### `require` fixtures

Install

```
npm install @mapbox/evilmvt --save
```

You can require the fixtures directly from the `evilmvt` module using the name of the fixture.

```javascript
var fixtures = require('@mapbox/evilmvt').fixtures;
var buffer = fixtures['invalid-Tags-nonexistant-values'];
// do something with bufer
```