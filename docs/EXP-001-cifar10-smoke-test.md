# EXP-001 — CIFAR-10 pipeline smoke test

- Date: 2026-10-22
- Branch: `experiment/cifar10-smoke-test`
- Status: Completed; pipeline check only, not a paper reproduction
- Source code: Unmodified

## Purpose

Confirm that the DP-FedAdamW script can load CIFAR-10, initialize Ray, run one tiny ResNet-18 training round, and save its outputs.

## Environment

- Hardware: Acer Aspire A715-42G; NVIDIA GeForce GTX 1650, 4 GB VRAM
- Windows NVIDIA driver: 621.01
- WSL: Ubuntu 26.04.1
- Conda environment: `dp-fedadamw`
- Python: 3.8.20
- PyTorch: 2.4.1+cu121
- torchvision: 0.19.1+cu121
- Ray: 1.0.0
- protobuf: 3.20.3

## Configuration

- Algorithm: `DP-FedAdamW`
- Dataset/model: CIFAR-10 / ResNet-18 with BN
- Clients: 1; participation: 1.0; `p`: 1
- Communication rounds: 1; local epochs: 1; max local steps: 1
- Batch size: 8; learning rate: 0.001
- Privacy enabled; `dp_sigma`: 0.2; clipping threshold `C`: 0.2
- `alpha_value`: 0.1; seed: 42

## Command

`python DP_adamw.py --alg DP-FedAdamW --data_name CIFAR10 --CNN resnet18 --normalization BN --epoch 1 --num_workers 1 --selection 1 --p 1 --E 1 --K 1 --batch_size 8 --lr 0.001 --num_gpus_per 1 --privacy 1 --dp_sigma 0.2 --C 0.2 --preprint 1 --extname smoke-test`

## Result

- Exit code: 0
- Test accuracy: 9.5%
- Train loss: 2.30294
- Test loss: 2.30318
- CIFAR-10 client label histogram: `{6: 247, 0: 187, 1: 27, 2: 22, 9: 14, 5: 3}`

This one-client, one-step result only confirms that the pipeline ran. It is not meaningful accuracy evidence and must not be reported as reproducing the paper.

## Notes

- CIFAR-10 was downloaded to `./data`; the script’s initial CIFAR-10 loader uses `download=False`.
- Ray warned that the `DataWorker` actor serialized about 198.5 MB. Keep laptop tests small; larger experiments need stronger compute.
- Model, log, and result files are local outputs and are excluded from Git.