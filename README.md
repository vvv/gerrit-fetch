`gerrit-fetch` fetches specified changesets from Gerrit. This can be
useful for doing offline code review without access to the Gerit web
interface, or comparing differrent submitted changesets.

Gerrit allows you to fetch individual changes into the git repository
like this:

```
git fetch https://review.openstack.org/p/openstack-ci/git-review \
	refs/changes/84/5784/2
git checkout -b c/5784/2 FETCH_HEAD
```

`gerrit-fetch` can fetch the last patchset of a change, a particular
patchset, or all patchsets of a change.

For every fetched patchset a local branch is created. E.g.,

```
gerrit-fetch 5784/3
```

would create branch `c/5784/3`. Here 5784 is Gerrit changeset number
and 2 is patchset number.

You can then compare changesets with a simple

```
git diff c/5784/2 c/5784/3
```

if they have the same parent.

```
Usage: gerrit-fetch [{-n | --dry-run}] CHANGESET...
       gerrit-fetch {-c | --checkout} CHANGESET
Fetches Gerrit changesets into local branches.

Options:
   -n, --dry-run     Show the names of branches but do not create them.
   -c, --checkout    Fetch a changeset and checkout newly created branch
                     to the working tree.

Changeset format:
   CHANGE            the last patch set of the change
   CHANGE/PATCHSET   specific patch set of the change
   CHANGE/           all patch sets of the change (cannot be used with `-c')

Example:
   # Fetch patch set 3 of change 5942 into local branch 'c/5942/3'.
   gerrit-fetch 5942/3

Set `REMOTE' environment variable to specify git remote ('origin' by default).
```
