# (C) Copyright IBM Corporation 2018,2019.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM websphere-liberty:18.0.0.3-kernel

ARG REPOSITORIES_PROPERTIES=""

RUN if [ ! -z $REPOSITORIES_PROPERTIES ]; then mkdir /opt/ibm/wlp/etc/ \
  && echo $REPOSITORIES_PROPERTIES > /opt/ibm/wlp/etc/repositories.properties; fi \
  && installUtility install --acceptLicense \
    jsp-2.3 servlet-4.0 springBoot-2.0 transportSecurity-1.0 webSocket-1.1 \
  && mkdir /opt/ibm/wlp/usr/shared/resources/lib.index.cache \
  && ln -s /opt/ibm/wlp/usr/shared/resources/lib.index.cache /lib.index.cache \
  && if [ ! -z $REPOSITORIES_PROPERTIES ]; then rm /opt/ibm/wlp/etc/repositories.properties; fi \
  && rm -rf /output/workarea /output/logs

COPY server.xml /config/

RUN server start && server stop && rm -rf /output/resources/security/ /logs/* && chmod -R g+rwx /opt/ibm/wlp/output/*

