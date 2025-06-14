
# Segmentation Format Specification

## Root-Level Keys

- `meta`: General metadata about the annotation and capture context.
- `salta`: Internal database information (SALTA system).
- `segmentations`: A dictionary of one or more segmentation entries.

---

## `meta` Object

| Field               | Type            | Required | Description |
|--------------------|-----------------|----------|-------------|
| title              | string          | yes      | Name of the segmentation dataset |
| source_file        | string          | yes      | Filename of the corresponding media |
| duration           | float           | yes      | Duration of the media file |
| units              | string          | yes      | Time unit (e.g., "seconds") |
| annotators         | array of string | yes      | List of annotators |
| version            | string          | yes      | Format version |
| date_capture       | string          | optional | Date when media was recorded |
| datum_capture      | string          | optional | Duplicate or alternative capture date |
| datum_entered      | string          | yes      | Date the metadata was entered in DB |
| comment            | string          | optional | Free-text comment |
| link               | string          | optional | External project/media link |
| modality           | object          | yes      | Information about data modalities |

### `modality` Subfields

#### VIDEO (optional)
- `one_take` (boolean)
- `single_subject` (boolean)
- `homogeneous_background` (boolean)
- `good_lighting` (boolean)

#### AUDIO (optional)
- `channels` (integer)
- `raw_preprocessed` (string) — e.g., "raw" or "preprocessed"
- `subjective_quality` (integer, 1–7)

#### IMU (optional)
- `type` (string) — e.g., "wearable"
- `device_model` (string)
- `num_sensors` (integer)

#### CUSTOM (optional)
- `description` (string)

---

## `salta` Object

| Field             | Type   | Required | Description |
|------------------|--------|----------|-------------|
| project_id       | string | yes      | Unique project ID in SALTA |
| primary_category | string | yes      | Main category based on ontology |
| secondary_category | string | optional | Optional sub-category |
| date_entered     | string | yes      | Date this data entered SALTA |
| uploader_id      | string | yes      | User who submitted the data |

---

## `segmentations` Object

Each key (`segmentation0`, `segmentation1`, ...) contains:

| Field          | Type    | Required | Description |
|----------------|---------|----------|-------------|
| type           | string  | yes      | One of: "AUTO", "weighted", "annotated" |
| date           | string  | yes      | Date of segmentation |
| user_feedback  | integer | optional | Satisfaction rating (1–7) |
| segments       | array   | yes      | List of segments |

### Segment Entry

| Field | Type  | Required | Description |
|-------|-------|----------|-------------|
| start | float | yes      | Start time in seconds |
| end   | float | yes      | End time in seconds |
| label | string| optional | Optional label |

---

## Example `.json` File

```json
{
  "meta": {
    "title": "Sample Segmentation",
    "source_file": "performance_01.mp4",
    "duration": 120.0,
    "units": "seconds",
    "annotators": ["user_a"],
    "version": "1.0",
    "date_capture": "2023-05-12",
    "datum_capture": "2023-05-12",
    "datum_entered": "2023-05-14",
    "comment": "Captured during rehearsal",
    "link": "http://example.com/project",
    "modality": {
      "VIDEO": {
        "one_take": true,
        "single_subject": true
      },
      "AUDIO": {
        "channels": 2,
        "raw_preprocessed": "raw",
        "subjective_quality": 6
      }
    }
  },
  "salta": {
    "project_id": "proj_123",
    "primary_category": "gesture",
    "secondary_category": "duo",
    "date_entered": "2023-05-15",
    "uploader_id": "user123"
  },
  "segmentations": {
    "segmentation0": {
      "type": "AUTO",
      "date": "2023-05-15",
      "user_feedback": 5,
      "segments": [
        { "start": 0.0, "end": 10.5, "label": "intro" },
        { "start": 10.5, "end": 30.0 },
        { "start": 30.0, "end": 50.0, "label": "gesture A" }
      ]
    }
  }
}
```
