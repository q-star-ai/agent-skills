# Asset Integration

Use this reference when `drama-commentary-skill` needs supporting images or BGM.

The material layer is now treated as formally available.

## Formal sources

### Images

- internal library first
- Pexels as the formal external image source

### BGM

- internal library first
- Freesound as the formal external BGM source

Mixkit can still be used as a fallback ingestion path, but it is no longer the preferred formal source for the 202 production flow.

## Formal asset fields

Upstream material records may contain many fields, but the commentary layer should only trust these fields for final consumption:

- `final_public_url`
- `final_qiniu_key`
- `status`
- `upload_status`
- `license`

## Required filter

For production use, only consume records that satisfy all of these:

- `status == "approved"`
- `upload_status == "done"` or missing only because the record is clearly legacy
- `final_public_url` exists
- `final_qiniu_key` exists

## License rule

### Images

Use only assets whose source and license are acceptable under the current platform policy.

### BGM

Prefer:

- `cc0`
- `cc-by`

Avoid using:

- `cc-by-nc`
- `cc-by-nc-nd`
- unclear or missing license records

If `cc-by` is used, preserve attribution metadata for the downstream publishing layer.

## Fields to ignore

Do not treat these as final truth:

- `public_url`
- `qiniu_key`
- `upload_job`
- `cache_path`

They are useful during ingestion, not as the final production reference.

## Default selection order

### Images

1. approved internal image
2. approved Pexels image

### BGM

1. approved internal BGM
2. approved Freesound BGM

## Output expectation

When this skill returns selected assets, prefer a compact structure like:

```json
{
  "selected_images": [
    {
      "id": "img_xxx",
      "final_public_url": "http://demo.q-star.ink/...",
      "final_qiniu_key": "asset-center/...",
      "license": "pexels"
    }
  ],
  "selected_bgm": [
    {
      "id": "bgm_xxx",
      "final_public_url": "http://demo.q-star.ink/...",
      "final_qiniu_key": "asset-center/...",
      "license": "cc0"
    }
  ]
}
```

The commentary layer should work from this final, filtered view and avoid reinterpreting raw ingestion details.
