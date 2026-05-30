# mlops-bootcamp-dagshub-dvc

A minimal example repository that combines Git, DVC, and Dagshub-compatible remote storage for data versioning.

## Contents

- `data/`
  - `data.txt` — sample data file tracked by DVC
  - `data.txt.dvc` — DVC metadata for the tracked file
- `src/` — project source folder (placeholder)
- `requirements.txt` — Python dependencies

## Purpose

This repository shows how to:

- track file data with DVC
- keep DVC metadata in Git
- configure a Dagshub-compatible remote for DVC

## Setup

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Initialize Git and DVC if not already done:
   ```bash
   git init
   dvc init
   git add .dvc .dvcignore
   git commit -m "Initialize DVC"
   ```

## Tracking data with DVC

Add the sample data to DVC tracking:

```bash
dvc add data/data.txt
git add data/data.txt.dvc data/.gitignore
git commit -m "Track data with DVC"
```

DVC stores the file contents in the local cache (`.dvc/cache`) and keeps the small metadata file in Git.

## Updating tracked data

When the tracked file changes:

```bash
dvc add data/data.txt
git add data/data.txt.dvc
git commit -m "Update tracked data"
```

## Restoring data versions

Restore a previous data version from Git history:

```bash
git checkout <commit>
dvc checkout
```

This updates `data/data.txt` to the version recorded by DVC in the checked-out commit.

## Dagshub remote setup

This repo includes an example Dagshub-compatible DVC remote setup. Replace the placeholders with your own Dagshub repository and credentials.

```bash
dvc remote add origin s3://dvc

dvc remote modify origin endpointurl https://dagshub.com/<username>/<repo>.s3

dvc remote modify origin --local access_key_id <ACCESS_KEY_ID>

dvc remote modify origin --local secret_access_key <SECRET_ACCESS_KEY>
```

Verify the remote:

```bash
dvc remote list
```

## Push and pull data

Push tracked data to the Dagshub remote:

```bash
dvc push -r origin
git push origin main
```

Pull tracked data from the Dagshub remote:

```bash
dvc pull -r origin
```

## Workflow notes

- Track DVC metadata files in Git, not the raw data files.
- Keep DVC credentials local using `--local` so they are not committed.
- Use `dvc push` and `dvc pull` when sharing data through the remote storage.