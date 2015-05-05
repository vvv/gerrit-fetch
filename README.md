This script fetches specified changesets from Gerrit. This can be
useful for doing offline code review without access to the Gerit web
interface, or comparing differrent submitted changesets.

Gerrit allows you to fetch individual changes into the git repository
like this:

```
git fetch https://review.openstack.org/p/openstack-ci/git-review \
	refs/changes/84/5784/2
git checkout FETCH_HEAD
```

This script can fetch the last patchset of a change, a particular
patchset, or all patchsets of a change.

For every fetched patchset a local branch is created. E.g.,
`gerrit-fetch 5784/2` would create branch `c/5784/2`. Here 5784 is
Gerrit changeset number and 2 is patchset number.

You can then compare changesets with a simple

```
git diff change/5784/2 change/5784/3
```

(if they have the same parent).
