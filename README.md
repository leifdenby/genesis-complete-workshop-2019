# GENESIS toolkit course for COMPLETE workshop 2019

This repository contains a short course given as part of the COMPLETE project
[workshop on "Data and model integration in fluid
mechanics"](https://sites.google.com/view/workshop-imperial/programme) on using
the [GENESIS analysis toolkit](https://github.com/leifdenby/genesis) developed
during the [GENESIS](http://homepages.see.leeds.ac.uk/~earlcd/GENESIS/)
project. The toolkit enables the study of coherent structures in atmospheric
flows and is designed to for studying coherent boundary layer structures which
trigger convective clouds.

Intro slides are available
[here](http://homepages.see.leeds.ac.uk/~earlcd/GENESIS/files/presentations/GENESIS_course_-_COMPLETE_workshop.pptx).

## Getting started

The repository contains jupyter notebooks with exercises (in
[notebooks/](notebooks/)) and examples for using the
[luigi](https://github.com/spotify/luigi) analysis pipeline in the GENESIS
toolkit (in [using_luigi/](using_luigi/)). To work on either you will need an
example dataset which can be downloaded
[here](http://homepages.see.leeds.ac.uk/~earlcd/genesis-data/fixed_flux_noshear__imperial.tar.gz).

You'll need to [install the GENESIS
toolkit](https://github.com/leifdenby/genesis#genesis-toolkit-for-analysing-coherent-structures-in-atmospheric-flows).

To get started on the exercises you should clone this repository locally:

```bash
git clone https://github.com/leifdenby/genesis-complete-workshop-2019
```

To view the notebooks move into the `notebooks/` folder and start `jupyter`

```bash
cd notebooks/
jupyter notebook
```

Once you have completed the exercises have a look using the GENESIS toolkit
through the luigi pipeline available in GENESIS. Instructions are in
[using_luigi/README.md](using_luigi/README.md).
