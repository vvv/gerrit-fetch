`gerrit-fetch` downloads specified changesets from Gerrit. This can be
useful for doing offline code review without access to the Gerit web
interface, or comparing submitted changesets.

Gerrit allows you to fetch individual changes into the git repository
like this:

```
git fetch https://review.openstack.org/p/openstack-ci/git-review \
	refs/changes/84/5784/2
git checkout -b c/5784/2 FETCH_HEAD
```

`gerrit-fetch` can download the last patchset of a change, a particular
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
Usage: gerrit-fetch [-n | --dry-run] [(-m | --name) <prefix>] [-c | --checkout] <changeset>...
       gerrit-fetch {-h | --help}
Fetches Gerrit changesets into local branches.

Options:
   -n, --dry-run
       Show the names of branches but do not create them.

   -m <prefix>, --name <prefix>
       Append given prefix to the branch name.
       Usual branch name format is "c/<change>/<patchset>".
       With '-m' option it will be "<prefix>.c/<change>/<patchset>".
       This lets you add mnemonics to otherwise opaque numerical ids.
       ("What was the topic of c/7971/2? And of c/7987/1?
        I wish I remembered.")

   -c, --checkout
       Fetch a changeset and switch into the newly created branch.

Changeset format:
   CHANGE            the last patch set of the change
   CHANGE/PATCHSET   specific patch set of the change
   CHANGE/           all patch sets of the change

Examples:
   # Fetch patch set 3 of change 5942 into local branch 'c/5942/3'.
   gerrit-fetch 5942/3

   # Fetch the latest patch set (2) of change 7976 into local branch
   # 'spiel-st.c/7976/2' and switch to it.
   gerrit-fetch -m spiel-st -c 7976

Set `REMOTE' environment variable to specify git remote ('origin' by default).
```
