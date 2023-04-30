#
# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM gcr.io/deeplearning-platform-release/base-cpu
RUN apt-get update && apt-get -yq install locales locales-all
COPY provision.sh /provision.sh
COPY provision/ /provision/
RUN bash -x /provision.sh
RUN sed -i -e 's/conda activate base/conda activate base\nconda activate silicon/' /entrypoint.sh
RUN sed -i -e 's@/opt/conda@/opt/conda/envs/silicon@' /run_jupyter.sh
ENV OPENLANE_ROOT=/OpenLane
ENV PDK_ROOT=/opt/conda/envs/silicon/share/pdk
ENV TCLLIBPATH=/opt/conda/envs/silicon/lib/tcllib1.20
ENV OL_INSTALL_DIR=/OpenLane/install
ENV OPENLANE_LOCAL_INSTALL=1
ENV PDK=sky130A
ENV STD_CELL_LIBRARY=sky130_fd_sc_hd
ENV STD_CELL_LIBRARY_OPT=sky130_fd_sc_hd
ENV PATH=$OPENLANE_ROOT:$OPENLANE_ROOT/scripts:$PATH
RUN apt-get update && apt-get -yq install imagemagick libcairo2-dev tcllib tklib make g++ libreadline-dev python3-cairosvg python3 python3-numpy libblas-dev ngspice z3 tcl8.6-dev tk8.6-dev python3-scipy python3-matplotlib texlive-latex-recommended unzip glpk-utils libglpk-dev python3-pulp git wget gauche python3-toml python3-pytoml python3-pip mmv libglu1-mesa-dev libcurl4-gnutls-dev pdf2svg python3-yaml python3-cffi python3-pyparsing python3-certifi tcl magic libsqlite3-dev python3-setuptools python3-networkx python3-sympy
RUN git clone https://github.com/thesourcerer8/StdCellLib
RUN git clone https://codeberg.org/Sourcerer/lclayout
RUN cd lclayout && ./install_develop.sh
