# Docker Image
```bash
# Note: it is in detach mode
docker run -d --gpus all -it --rm --network=host --ipc=host --shm-size=16g --ulimit memlock=-1 --ulimit stack=67108864 \
    vuiseng9/mlperfv6.0-nebius-b300-n1-gpt-oss
```
or build
```bash
git clone https://github.com/vuiseng9/mlperf-train-v6.0
cd mlperf-train-v6.0/Nebius/benchmarks/gpt_oss_20bNebius/benchmarks/gpt_oss_20b && git checkout 260619-local
docker build --no-cache -t vuiseng9/mlperfv6.0-nebius-b300-n1-gpt-oss .
```

# Run 
```bash
# gpt-oss on 8xb300 

# Note: we use synthetic dataset to bypass huge dataset download
# verify performance by checking training step time against submitted results.

cd /workspace/llm
export USE_SYNTHETIC_DATA=1
source configs/nebius_b300_n1/config_DGXB300_1x8x3xtp1pp1cp1ep1_mxfp8.sh
bash ./run_and_time.sh

# export DBG_ATTACH=1 to use debugpy
```