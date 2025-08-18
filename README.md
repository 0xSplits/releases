# releases

In this repository we define the versions of our offchain services that are
running in any given environment. Below some rules of thumb to remember for
working with releases at Splits.

- branches are environments, except for `production`, there is no production branch
- `production` is being deployed by creating Git tags, e.g. via Github releases
- the default branch does always describe the `staging` environment

### Environments

The following environments exist today based on their respective naming
conventions. We can add and remove permanent test environment if need be.

- `development` aka `dev`: this is your machine, localhost etc, we run docker compose here
- `testing` aka `test`: this is the cloud, AWS etc, first line of defense via integration tests etc
- `staging` aka `stage`: this is the cloud, AWS etc, second line of defense via smoke tests etc
- `production` aka `prod`: this is the cloud, AWS etc, we live and die by the sword here

### Schema

Releases must be defined in the [./infrastructure/](./infrastructure/) and
[./service/](./service/) folders, which may contain nested folder structures
themselves. If you want to change the way release definitions are loaded, then
have a look at [this pull request](https://github.com/0xSplits/kayron/pull/45),
where the release loader whitelist got introduced.

Our proprietary release schema is define by our deployment operator Kayron in
[./pkg/release/schema](https://github.com/0xSplits/kayron/tree/main/pkg/release/schema).
If you want to modify the way releases are defined, then you have to make sure
Kayron can find and interpret the desired schema changes.

```
- docker: "specta"
  github: "specta"
  deploy:
    release: "v0.1.16"
```
