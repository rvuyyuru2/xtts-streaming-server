FROM pytorch/pytorch:2.1.0-cuda12.1-cudnn8-devel
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --no-install-recommends -y sox libsox-fmt-all curl wget gcc git git-lfs build-essential libaio-dev libsndfile1 ssh ffmpeg && \
    apt-get clean && apt-get -y autoremove


COPY . /app
WORKDIR /app
RUN python -m pip install --use-deprecated=legacy-resolver -r requirements.txt \
    && python -m pip cache purge
RUN ls
RUN python -m unidic download
RUN mkdir -p /app/tts_models



#Mark this 1 if you have older card
ENV NVIDIA_DISABLE_REQUIRE=0
ENV COQUI_TOS_AGREED=1 


EXPOSE 8020

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8020"]
