# Copyright 2018 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder
RUN apt-get update && apt-get install --no-install-recommends -y curl python3-pip python3-setuptools python3-wheel nasm && pip3 install meson ninja
RUN curl --silent -O https://storage.googleapis.com/aom-test-data/fuzzer/dec_fuzzer_seed_corpus.zip
RUN curl --silent -O https://jannau.net/dav1d_fuzzer_seed_corpus.zip
COPY . dav1d
RUN rm -rf dav1d/mayhem
WORKDIR dav1d
COPY mayhem/build.sh $SRC/
COPY mayhem/linux32.meson $SRC/

ENV FUZZING_LANGUAGE=c++ SANITIZER=address ARCHITECTURE=x86_64
RUN compile
RUN chmod +x /out/dav1d_fuzzer
