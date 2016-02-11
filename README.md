# git-mirror-resource

Takes the docker image from concourse/git-resource and modifies the
check/in/out scripts for mirrored clones.

Check will not clone anything, this would be a waste of bandwidth/resources,
instead it checks the remote is valid (by attempting to `git ls-remote`) and
returns a new version at a time based on the specified frequency.

This will not track changes to a branch/tag (nor any ref within a repo), instead
this will pass a new "version" onto Concourse.ci in the format
"{'updated': 'YY-MM-DD'}".

## Config

`uri`, `skip_ssl_verification`, `private_key` follow the same format as used by
the git-resource, the only new field is `frequency`:

* `frequency`: *Optional.* How often a new version should be reported
  (daily|weekly|monthly), defaults to daily.
