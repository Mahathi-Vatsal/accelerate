# Copyright (c) 2024 Intel Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# SPDX-License-Identifier: Apache-2.0

# Use a Python slim base image
FROM python:3.10-slim

# Set up non-interactive mode for APT
ENV DEBIAN_FRONTEND=noninteractive

ENV NO_PROXY=""
ENV no_proxy=""

# Install necessary system dependencies
RUN apt-get update && apt-get install -y wget git && rm -rf /var/lib/apt/lists/*

# Install PyTorch, IPEX, OneCCL, and Accelerate in a single RUN command
RUN python -m pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu && \
    python -m pip install intel-extension-for-pytorch && \
    python -m pip install oneccl_bind_pt --extra-index-url https://pytorch-extension.intel.com/release-whl/stable/cpu/us/ && \
    pip install accelerate

RUN git clone https://github.com/Mahathi-Vatsal/accelerate.git && \
    cd accelerate && \
    pip install . &&\
    pip install -r kubernetes/requirements.txt
