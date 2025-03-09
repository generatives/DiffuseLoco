# DiffuseLoco

## Evaluate Pre-trained Checkpoints

```bash
source env.sh
```

Bipedal Walking Task

```bash
python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_stand \
--online=false --generate_data=true
```

Self trained policy:

```bash
python ./scripts/eval.py --checkpoint=./outputs/2025-03-09/11-25-54/checkpoints/latest.ckpt --task=cyber2_stand
```

Hop Task

```bash
python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_hop
```

Bounce Task

```bash
python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_bounce
```

Walk Task

You will be able to see the probabilistic policy executing both trotting and pacing in different envs given the same command

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_walk \
# --online=false --generate_data=true
```

## Dataset Generation

To generate the dataset from source RL checkpoints for each task, run the following command:

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=<TASK_NAME>
--online=false --generate_dataset=true
```

Then, use `scripts/combine_dataset.py` to combine the generated datasets (`skill_filenames` should be modified).

After that, you can use `scripts/train.py` to train the diffusion model.

**NOTE**:

- Looks like only `cyber2_stand.pt` source RL policy available for now.
- Names of datasets should be adapted in `scripts/combine_dataset.py` and `diffusion_policy/config_files/cyber_diffusion_policy_medium_model.yaml`.
- Change the record length by editing var `len_to_save` in `diffusion_policy/diffusion_policy/env_runner/cyber_runner.py`
- Condition dims are not match in the original codes, therefore set it to `cond_dim: 45` in `cyber_diffusion_policy_medium_model.yaml`
- Comment out this to avoid infinity rolling out in `diffusion_policy/diffusion_policy/env_runner/cyber_runner.py`
  ```
  # run rollout
  # if (self.epoch % cfg.training.rollout_every) == 0:
  ```
- There are **ghost values** in `diffusion_policy/diffusion_policy/env_runner/cyber_runner.py`, such as `num_envs`, which should be considered.

## Training

```bash
source env.sh

python scripts/train.py
```

Currently dataset generation is still pending.
