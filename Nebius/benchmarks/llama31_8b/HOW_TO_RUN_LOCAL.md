# Docker Image
```bash
# Note: it is in detach mode
docker run -d --gpus all -it --rm --network=host --ipc=host --shm-size=16g --ulimit memlock=-1 --ulimit stack=67108864 \
    vuiseng9/mlperfv6.0-nebius-b300-n1:llama31_8b-pyt
```
or build
```bash
git clone https://github.com/vuiseng9/mlperf-train-v6.0
cd mlperf-train-v5.1 && git checkout 260619-local
docker build --no-cache -t mlperfv6.0-nebius-b300-n1:llama31_8b-pyt .
```

# Run 
```bash
# llama31_8b on 8xb300 

# Note: we use synthetic dataset to bypass huge dataset download
# verify performance by checking training step time against submitted results.

cd /workspace/llm
export USE_SYNTHETIC_DATA=1
source configs/nebius_b300_n1/config_DGXB300_1x8x2xtp1pp1cp1_8b_fp4.sh
bash ./run_and_time.sh

# add DBG_ATTACH=1 to use debugpy
```