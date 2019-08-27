FROM rakeshchoyal92/unity3d:latest As builder

ENV UNITY_PATH='/opt/Unity/Editor/Unity'

ARG LICENSE_FILE=Unity_lic.ulf
ARG PROJECT_PATH=/root/project
ARG BUILD_SCRIPT=Buildscript.Build
ARG LOGFILE=./logs/build.log
ARG UNITY_ARGS='-quit -batchmode -nographics'

WORKDIR /root/project
COPY . .

COPY ${LICENSE_FILE} /root/.local/share/unity3d/Unity/Unity_lic.ulf
RUN ${UNITY_PATH} ${UNITY_ARGS} ${PROJECT_PATH} -executeMethod ${BUILD_SCRIPT} -logFile

RUN pwd
RUN ls
RUN ls /root/project

FROM nginx
COPY --from=builder /root/project/build /usr/share/nginx/html
