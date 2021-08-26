# devspace-multiple-sync-poc

To reproduce:
- run `devspace dev`
- to check downstream sync from `foo` container only:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c foo -- sh -c 'echo foo >> /tmp/sync/foo/foo.tmp'
  ```
  (This works: only downloads the file from the `foo` container)
- to check downstream sync from `bar` container only:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c bar -- sh -c 'echo bar >> /tmp/sync/bar/bar.tmp'
  ```
  (This works: only downloads the file from the `bar` container)
- to check downstream sync from `foo` in a shared container dir:
  ```
  devspace enter -l app=rh-devspace-multiple-sync-poc -c foo -- sh -c 'echo foo >> /tmp/sync/shared/shared.tmp'
  ```
  (This works: downloads the file from the `foo` container, and then uploads the file to the `bar` container)
- to check upstream sync to `foo` container only:
  ```
  echo foo >> src/foo/foo.tmp
  ```
  (This works: only uploads the file to the `foo` container)
- to check upstream sync to `bar` container only:
  ```
  echo bar >> src/bar/bar.tmp
  ```
  (This does *NOT* work: Doesn't upload the file to the `bar` container)
- to check upstream sync to both containers:
  ```
  echo shared >> src/shared/shared.tmp
  ```
  (This works: uploads the file to both containers)

Which container's sync works seems to be unpredictable: sometimes, uploads to only `foo` don't work, sometimes it's uploads to `bar`.
