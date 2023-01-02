
## v0.8.0
* Improve templates to inherit values from drom.toml/package.toml inherited
   files
* drom_toml: because `drom` requires additional features in toml that do not
   fit in the standard `toml` library, we forked `toml.0.7.1` into `drom_toml`.
   Additional features:
   * New operators: == (init value if never set), := (override value),
       -= (delete/clear value)
* Fix ocamlformat stuck at 0.15
* Make .ocamlformat-ignore always ignore share-dirs

## v0.7.0
* temporary version, never released

## v0.6.0
* Generate opam files in opam/ instead of top directory
* `drom install PACKAGES` where PACKAGES is a limited set of project packages
* `drom build` tries to update program files by default, unless
   `auto-upgrade: false` is set in user configuration:
   ```
   [user]
   auto-upgrade = false
   ```

## v0.5.0
* Add --edition and --min-edition to `drom new` and `drom project`
* Add support for optional dependencies:
  lib = { opt = true, version = "3.1" }
* Add @ before skip tags: skip = [ "@test" ]
* drom uninstall: also unpin all project packages
* Add support for optional packages:
  optional = true
* Add support for preprocessor
  preprocess = "pps pgocaml_ppx"

## v0.4.0 ( 2021-05-11 )
* New [fields] in package.toml:
  * 'gen-opam' to generate the opam file of a virtual package. Possible values
    are "all" (all sub-packages are dependencies), "some" (you need to specify
    the dependencies in [dependencies]) or "none" (no opam file is generated,
    the default).
  * 'no-opam-test = "no"' to disable tests in the opam package
  * 'no-opam-doc = "no"' to disable doc in the opam package
* Add 'rust_binding' skeleton
* New env variable DROM_VERBOSE_SUBST to debug substitutions
* New 'skip = [ "file"...]' in package.toml to skip files in src/PACKAGE/
* New subcommand 'list': "drom list" will list all known skeletons. If
  an argument is provided, it is either "all", or one of "projects" or
  "packages".

## v0.3.0
* More skeletons

## v0.2.1 ( 2020-11-25 )

* Add table `[file]` in `skeleton.toml` to specify flags for skeleton files
    from the outside (useful for binary files for example). Flags can be
    `file` (name of file), `create` (create only if non-existing), `skips`
    (list of tags forcing skip), `subst` (do not perform substitution)
* Extend skeleton substitution language with ![if:COND]...![else]...![fi]
    COND can be `gen:SKIPTAG`, `skip:SKIPTAG`, `skeleton:is:SKELETON`,
    `kind:is:KIND`, `not:COND`, `pack` (packed)
* New skeleton projects `mini-lib` and `mini-prg` with
   `skip = "test sphinx github docs ocamlformat ocp-indent code"`
* Improved inline documentation of `drom.toml` and `package.toml` files
* New command `drom opam-plugin` to install `drom` as an opam plugin, so it
  can be called `opam drom` from anywhere.
* New argument `--profile PROFILE` to `drom build`
* New argument `--all` to `drom test` to do the test on all available/compatible
   opam switches (using dune-workspace context feature)
* New option `dev-tools` in ~/.config/drom/config, a list of opam packages
   that should be installed in the local switch when `drom dev-deps` is called
* New environment variable DROM_SHARE_DIR can be used to set the directory
   containing `skeletons` and `licenses` directories (can be used to install
   drom globally, i.e. DROM_SHARE_DIR=$OPAM_SWITCH_PREFIX/share/drom)
* New common argument `-q` or `--quiet` to set verbosity to 0
* New command `drom dep [DEP]`: display and update dependencies with options:
  --package NAME : only for package NAME
  --tool : tool dependencies
  --add : add new dependency
  --remove : remove dependency
  --ver VERSION : set version constraint
  --lib LIBNAME : set dune name
  --test BOOL : set for-test
  --doc BOOL : set for-doc
* New option `drom package x --new-file y.ml` to create a source file with
  a correct license header
* Field `gen-version = "version.ml"` in `package.toml` does not create the
   file "version.ml" anymore, but a script "version.mlt" to generate the
   file with git information
* New command `drom lock` to generate a file `${package}-deps.opam.locked`
  and git add it.
* New argument `--locked` to `drom build` to use `${package}-deps.opam.locked`
  if available.
* Fixes:
  * OCaml escaping in toml file preventing `drom new` when utf8 chars are
    present in email addresses of authors

## v0.2.0 ( 2020-11-24 )

* Fix bug with misnamed 'packages.toml` file in skeletons

## v0.1.0 ( 2020-11-23 )

* First version

