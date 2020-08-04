# jclulow Ergodox EZ firmware

This branch contains the keyboard layout I'm using on my Ergodox EZ.

Rough notes on use:

```
sudo apt install avr-libc gcc-avr teensy-loader-cli
python3 -m ../venv
. ../venv/bin/activate
pip install wheel
pip install -r requirements.txt
./bin/qmk compile -kb ergodox_ez -km jclulow
./bin/qmk flash -kb ergodox_ez -km jclulow
```

Note that in this layout, the reset button is top-right in Layer 2.

# ZSA's fork of QMK Firmware 

This purpose of this fork is maintain a clean repo that only contains the keyboard code that we need, and as little else as possible.  This is to keep it lightweight, since we only need a couple of keyboards. This is the repo that the EZ Configurator will pull from. 

## Supported Keyboards

* [Planck](/keyboards/planck/ez)
* [ErgoDox EZ](/keyboards/ergodox_ez/)

## Maintainers

QMK is developed and maintained by Jack Humbert of OLKB with contributions from the community, and of course, [Hasu](https://github.com/tmk). The ZSA branch is maintained by Drashna, ZSA's official QMK Liaison, and by Florian Didron, ZSA's lead developer, with input from Erez Zukerman (ZSA CEO).


# Update Process

1. Check out branch from ZSA's master branch:
    1. `git remote add zsa https://github.com/ErgoDox-EZ/qmk_firmware.git`
    2. `git fetch --all`
    3. `git checkout -B branchname zsa/master`
    4. `git push -u zsa branchname`
2. Check for core changes:
    - [https://github.com/qmk/qmk_firmware/commits/master/quantum](https://github.com/qmk/qmk_firmware/commits/master/quantum)
    - [https://github.com/qmk/qmk_firmware/commits/master/tmk_core](https://github.com/qmk/qmk_firmware/commits/master/tmk_core)
    - [https://github.com/qmk/qmk_firmware/commits/master/util](https://github.com/qmk/qmk_firmware/commits/master/util)
    - [https://github.com/qmk/qmk_firmware/commits/master/drivers](https://github.com/qmk/qmk_firmware/commits/master/drivers)
    - [https://github.com/qmk/qmk_firmware/commits/master/lib](https://github.com/qmk/qmk_firmware/commits/master/lib)
    - These folders are the important ones for maintaining the repo and keeping it properly up to date. Most, but not all, changes on this list should be pulled into our repo.
3. `git cherry-pick` the commits we want
    - `git rm docs/* -r` to remove the document updates when cherry picking. Repeat for any keyboard/keymap/etc that have changes that we aren't interested in
4. Commit update
   * Include commit info in `[changelog.md](http://changelog.md)` 
5. Open Pull request, and include information about the commit

## Strategy

To keep PRs small and easier to test, they should ideally be 1:1 with commits from QMK Firmware master. They should only group commits if/when it makes sense. Such as multiple commits for a specific feature (split RGB support, for instance)

## Merging

Pull Requests should be merged/rebased, not squashed, so we can maintain a commit history that is close to QMK Firmware's, for ease of reference.
