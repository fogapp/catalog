# fog-apps

The apps built for [fog](https://github.com/fogapp/fog): Fin, Hub, Office,
Stream, Feed, Hook, Once, HUD, Lucid, Newtab, Signet, Fit and think fleet.
Every fog reads this catalog out of the box, and its apps install directly.

This is a `fog-catalog/1` catalog. The format is fog's
`docs/catalog-contract.md`.

```
catalog.yaml          name, what's featured, display order
apps/<id>/app.yaml    one app: spec, install options, listing, footprint
apps/<id>/tile.svg    its tile
```

## Where the apps are built from

Each entry is built from its own repository (`firstParty: <repo>`). The
clone URL comes from the fog's settings, under Settings › App store ›
First-party app source: a base such as `ssh://git@git.example.com/you/`,
plus `<repo>.git`, or a per-app override. An entry's `publicRepo`, once an
app is published, lets a fog with no base install it too. A fog with
neither leaves the app out of its store.

## Keeping an entry in step with its app

Each app's repository has its own manifest, `<repo>/<id>.fog.yaml`. The
entry here is a copy of its spec, and that copy is what a one-click install
deploys. When the two drift, a store install quietly differs from the app
its author ships. fog's tests check every entry against its manifest field
by field. They run when this repository, `fog-catalog`, and the app
repositories are checked out beside fog:

```sh
cd ../fog && go test ./internal/catalog
```

Change the manifest and the entry together, then push this repository.
Fogs pick it up at their next fetch.
