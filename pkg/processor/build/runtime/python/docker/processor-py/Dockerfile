# Copyright 2017 The Nuclio Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG NUCLIO_PYTHON_VERSION=3
ARG NUCLIO_PYTHON_OS=alpine3.6

#
# Build stage: builds the processor binary
#

FROM nuclio/processor as build

#
# Output stage
#

FROM python:${NUCLIO_PYTHON_VERSION}-${NUCLIO_PYTHON_OS}

COPY --from=build /go/src/github.com/nuclio/nuclio/processor /usr/local/bin/processor
COPY pkg/processor/runtime/python/wrapper.py /opt/nuclio/wrapper.py

# generate a version file
ARG NUCLIO_VERSION_INFO_FILE_CONTENTS
RUN mkdir -p /etc/nuclio && echo ${NUCLIO_VERSION_INFO_FILE_CONTENTS} > /etc/nuclio/version_info.json
