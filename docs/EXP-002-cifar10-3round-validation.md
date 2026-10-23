# EXP-002 — CIFAR-10 3-round validation attempt

- Date: 2026-10-22
- Status: Failed/incomplete; not a paper reproduction
- Configuration: CIFAR-10, ResNet-18, DP-FedAdamW, 1 client, 3 rounds, batch size 8
- Outcome: No completed round results; do not report accuracy or loss.
- Error: Ray worker died after the local node missed heartbeats; failure occurred at `ray.get`.
- Notes: Laptop remained on. Ray warned that the DataWorker actor was about 198.5 MB. The Linux log check found no out-of-memory kill.
- Conclusion: The run stopped because Ray/WSL became unresponsive; the exact cause is unknown. This does not establish an algorithm failure.
- Next: Diagnose Ray/WSL before retrying.