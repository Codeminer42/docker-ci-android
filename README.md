# Codeminer42 Android Image for CI builds

Docker Android images used by Gitlab CI.

## Dependencies

The following dependencies are being installed on all images:

* Android 26 sdk for linux
* Android Emulator

## Tags

We currently have images for the following Android versions.

### Android images

- `26`, `latest` [Dockerfile](https://github.com/Codeminer42/docker-ci-android/blob/master/26/Dockerfile)

## Contributing

`Dockerfiles` are stored under folders for each version.

For updating the images, just open a _pull request_ with
the new `Dockerfile` version and, after accepted, Docker
Hub will build automatically after a few minutes.

The images should setup an environment that is widely used,
please don't install dependencies that are specific to a
project. It's also good to have a pattern and all images
support the same things.
