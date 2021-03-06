gowrk
=====

Helper script for working on multiple open-source Go packages in a single
workspace.

### Starting new workspace

  * Fork and clone gowrk

  `git clone git@bitbucket.org:you/gowrk.git mywrk`

  * Create your workspace branch

  `git checkout -b workspace`

  * Add projects you're going to work on

```bash
cd mywrk; mkdir -p src/bitbucket.org/you
git submodule add git@bitbucket.org:you/project1.git src/bitbucket.org/you/project1
git submodule add git@bitbucket.org:you/project2.git src/bitbucket.org/you/project2
git commit -a -m "created new worksapce"
```

### Usage

```
usage: gowrk up        | commit submodules HEADs
       ----------------+------------------------------
       gowrk lint      | check code style
       gowrk           | runs go test -race over any
                       | package added as a submodule
                       | under ./src directory
       gowrk verbose   | same as above plus does not
                       | suppress stdout nor stderr
       gowrk 'reg.*ex' | tests packages that match
                       | pattern; can be combined with
                       | verbose
       ----------------+------------------------------
       gowrk help      | print this help message
```

  * Customize your workspace with source scripts

    Every time gowrk is sourced in your current shell it sources
    also .gowrkrc and/or any .gowrkrc.d/* script it can find. By
    sourcing gowrk in your current shell you ensure proper GOPATH
    and GOBIN env vars are exported.

  `cd mywrk; . gowrk`

  * Run tests for your projects

  `cd mywrk; gowrk`

  * Update mywrk submodule refs after any commits/pushes you done
    in your projects:

```bash
cd mywrk/src/github.com/you/project1;
git commit Readme.md -m"initial commit"
git push origin master
cd ${GOPATH}
gowrk up; git push
```

### MacOSX note

  gowrk uses GNU Readlink, you may want to install it first

```
brew install coreutils
```

### License

Distributed under the MIT license, see License.md for details.

