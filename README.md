# conda_wxpython
Recipe for building wxPython 3.0.2 on linux

# Instructions:
1. cd recipe
2. docker build .
3. create container with new image (`docker create <image>`)
4. copy directory to local directory (`docker cp <container>:/opt/conda/envs/build/conda-bld/linux-64 ./tmp`)
5. upload to anaconda.org (on local `conda-build` environment, `anaconda upload -u cctbx <file>`)
