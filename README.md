# mlops-bootcamp-dagshub-dvc

A first version of the repository that demonstrates a basic DVC workflow with a tracked data file.

This repo is not the final Dagshub-enabled project yet; it currently focuses on explaining how DVC works alongside Git.

## Contents

- `data/`
  - `data.txt` - sample data tracked by DVC
  - `data.txt.dvc` - DVC metadata for the tracked file
- `src/` - project source folder (empty placeholder)
- `requirements.txt` - Python dependencies

## Purpose

This repository is meant to show how DVC can be used alongside Git to version data files without checking the raw data itself into Git.

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

To add a file to DVC tracking:

```bash
dvc add data/data.txt
git add data/data.txt.dvc
git add data/.gitignore
git commit -m "Track data with DVC"
```

DVC stores the actual file contents in the cache (`.dvc/cache`) and keeps a small metadata file (`data/data.txt.dvc`) in Git.

## Updating tracked data

When the tracked file changes:

```bash
dvc add data/data.txt
git add data/data.txt.dvc
git commit -m "Update tracked data"
```

## Restoring data versions

Use Git history together with DVC to restore a previous data version:

```bash
git checkout <commit>
dvc checkout
```

This updates the working copy of `data/data.txt` to match the DVC metadata in the checked-out commit.

## Notes

- Git should track the `.dvc` metadata files, not the large data files themselves.
- DVC manages the data file contents and the hash mapping inside `.dvc/cache`.
- If you use a remote DVC storage, configure it with `dvc remote add` and `dvc push`.
- Dagshub integration will be added later; this version is focused on getting the DVC workflow in place first.
 

 ----------------


Dagshub: remote repositories to track everything. 
Conceptual model: GitHub for code, DVC for data, MLflow for models, Dagshub remote repository.

Dagshub: same as Git. We can create a blank repo in dagshub.com, and then clone it here using the URL

Dagshub supports: 1) data, 2) code, 3) experiments

We can connect to any cloud storage bucket.

python library: dagshub

How to add to the Dagshub remote repository the tracking of the data with DVC (commands in the Data section of the Dagshub repository):
- Set up the Dagshub DVC remote: dvc remote add origin s3://dvc
- Connect to the Dagshub repo: dvc remote modify origin endpointurl https://dagshub.com/munozgonzalez4/mlops-bootcamp-dvc-intro.s3
- Set up security credentials: 
    - dvc remote modify origin --local access_key_id 977de0b62cda70873102f4db3f76e69c926d66e6
    - dvc remote modify origin --local secret_access_key 977de0b62cda70873102f4db3f76e69c926d66e6

Test: dvc remote list

Pull: dvc pull -r origin
Push: 
    - dvc push -r origin
    - git push origin main


When doing changes in the data:
dvc add data/data.txt
git add .
git commit -m "message"
dvc pull -r origin
dvc push -r origin
git push origin main

