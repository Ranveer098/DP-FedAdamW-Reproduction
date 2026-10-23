# EXP-003 — Colab CIFAR-10 3-round smoke test

- Date: 2026-10-23
- Status: Completed; pipeline check only, not a paper reproduction
- Repository branch: `experiment/cifar10-smoke-test`
- Hardware: Google Colab Tesla T4, 15 GB VRAM
- Environment: Python 3.13.15, PyTorch 2.11.0+cu130, torchvision 0.26.0+cu130, Ray 2.59.0, NumPy 2.1.3
- Temporary compatibility workaround: In the Colab copy only, set Ray's `FUNCTION_SIZE_ERROR_THRESHOLD` to 256 MiB so it would accept the 189 MiB `DataWorker`. This was not pushed to GitHub.

## Configuration

CIFAR-10, ResNet-18 with BN, DP-FedAdamW; 1 client; 3 communication rounds; 1 local epoch; K=1; batch size 8; learning rate 0.001; privacy enabled; C=0.2; dp_sigma=0.2; seed=42.

## Command

```bash
python DP_adamw.py --alg DP-FedAdamW --data_name CIFAR10 --CNN resnet18 --normalization BN --epoch 3 --num_workers 1 --selection 1 --p 1 --E 1 --K 1 --batch_size 8 --lr 0.001 --num_gpus_per 1 --privacy 1 --dp_sigma 0.2 --C 0.2 --preprint 1 --extname colab-raylimit-smoke2