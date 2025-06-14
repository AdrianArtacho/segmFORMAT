
# Segmentation Format

This repository/document defines a JSON (and YAML-compatible) format for storing segmentation and annotation data for multimodal performance recordings.

## Contents

- `segmentation_format_specification.md` — Human-readable format spec
- `segmentation_format_specification.yaml` — Example file in YAML format
- `segmentation_format_specification.tex` — LaTeX documentation (field-by-field spec)

## Format Overview

The format is structured around three root keys:

- `meta`: Metadata about the media file and its capture context
- `salta`: Internal system info, categories, and project metadata
- `segmentations`: One or more segmentations, each with a list of temporal segments

## Supported Modalities

The `modality` field supports the following subfields:

- `VIDEO`: boolean flags like `one_take`, `homogeneous_background`
- `AUDIO`: attributes like `channels`, `raw_preprocessed`, `subjective_quality`
- `IMU`: description of sensor setup
- `CUSTOM`: any user-defined modality

## Segmentations

Each segmentation includes:

- `type`: e.g. `AUTO`, `weighted`, or `annotated`
- `date`: when segmentation was made
- `user_feedback`: optional satisfaction score (1–7)
- `segments`: list of segments with `start`, `end`, and optional `label`

## Example Use Case

See `segmentation_format_specification.yaml` for a working example using video and audio modality annotations.

## License

MIT License — Free to use and adapt for your research or projects.
