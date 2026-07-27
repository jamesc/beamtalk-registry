# beamtalk-registry

The default package registry index for [Beamtalk](https://github.com/jamesc/beamtalk).

This repository has no code — it is a lookup table from package name + version to a
git repository and tag, read by the Beamtalk CLI's `deps` and `publish` commands. See
[Package Registry](https://github.com/jamesc/beamtalk/blob/main/docs/beamtalk-packages.md#package-registry)
in the main repo's docs for the full format.

## Publishing

Publish a release from your package's own repository — do not edit this repository
by hand:

    beamtalk version bump minor   # or `beamtalk version X.Y.Z`
    git add beamtalk.toml && git commit -m "release 0.3.0"
    beamtalk publish

`beamtalk publish` tags your repository, pushes the tag, and opens (or updates)
`packages/<your-package>.toml` here on your behalf, provided you have push access
to this repository (or the `[registry] url` in your project points at a fork or
private mirror you do have access to).

## Layout

    packages/
      <name>.toml   # one file per published package — see the template linked above

## Using a package

Add a bare-string dependency to your project's `beamtalk.toml` — the version is an
exact `major.minor.patch`, resolved through this index into a git repository and tag:

```toml
[dependencies]
yaml = "0.1.0"
```

Or let the CLI pin the latest published release for you:

    beamtalk deps add yaml

## License

Apache-2.0 — see [LICENSE](LICENSE). The index entries here are metadata only;
each package is licensed by its own repository.
