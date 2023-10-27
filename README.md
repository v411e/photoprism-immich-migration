[![PyPI version](https://badge.fury.io/py/ppim-migrator.svg)](https://badge.fury.io/py/ppim-migrator)
# Photoprism to Immich migrator
This tool can migrate albums and favorites from Photoprism to Immich. It does not migrate you photos.

## Prerequisites
The tool will only work if you keep the same file structure in immich that you already had in photoprism.
This is the case if you take the `original` folder from photoprism and use it in immich as external library.

## How it works
### Migrate favorites
1. The tool fetches all photos with a `favorite` tag from your photoprism instance
2. For each photo, it retrieves the original `filename` and its respective `path`
3. It connects to immich, tries to find the photo by `filename` and validates potential candidates on the immich side by comparing the file `path`
4. If a match was found, it marks the photo on immich as `favorite`

### Migrate album
1. The tool fetches all photos of a certain `album` from your photoprism instance
2. For each photo, it retrieves the original `filename` and its respective `path`
3. It connects to immich, tries to find the photo by `filename` and validates potential candidates on the immich side by comparing the file `path`
4. If a match was found, it creates a new `album` in immich and adds the matched photos

## Installation
```
pip install ppim-migrator
```

## Configuration
Create a `config.yaml` file in the working directory where you want to run the command.
```
photoprism:
  base_url: https://photoprism.example.com
  username: 
  password: 
immich:
  base_url: https://immich.example.com
  api_key: 
```

## Usage
### Migrate all favorites from photoprism to immich
```
python -m ppim-migrator migrate-favorites
```

### Migrate a certain album from photoprism to immich
To get an `album-id` just open the album in photoprism. The id is part of the url. 
Example:
- Url, when opening the album: `https://photoprism.example.com/library/albums/aqrcixa2uf1q45iq/view`
  The `album-id` would be `aqrcixa2uf1q45iq`
```
python -m ppim-migrator migrate-album <album-id-here>
```
