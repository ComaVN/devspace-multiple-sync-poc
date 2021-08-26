# devspace-multiple-sync-poc

To reproduce:
- run `devspace dev`
- to check downstream sync from `foo` container only:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c foo -- sh -c 'echo foo >> /tmp/sync/foo/foo.tmp'
  ```
- to check downstream sync from `bar` container only:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c bar -- sh -c 'echo bar >> /tmp/sync/bar/bar.tmp'
  ```
- to check downstream sync from `foo` in a shared container dir:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c foo -- sh -c 'echo foo >> /tmp/sync/shared/shared.tmp'
  ```
- to check upstream sync to `foo` container only:
  ```
  echo foo >> src/foo/foo.tmp
  ```
- to check upstream sync to `bar` container only:
  ```
  echo bar >> src/bar/bar.tmp
  ```
- to check upstream sync to both containers:
  ```
  echo shared >> src/shared/shared.tmp
  ```
