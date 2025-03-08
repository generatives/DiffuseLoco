# DiffuseLoco

## Evaluate Pre-trained Checkpoints

Bipedal Walking Task

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_stand \
--online=false --generate_data=true
```

Hop Task

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_hop
```

Bounce Task

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_bounce
```

Walk Task

You will be able to see the probabilistic policy executing both trotting and pacing in different envs given the same command

```bash
source env.sh

python ./scripts/eval.py --checkpoint=./cyberdog_final.ckpt --task=cyber2_walk \
# --online=false --generate_data=true
```



**NOTE**:

- If `online` is set to false, source ckpt will be loaded.
- To generate training data, set `online` to `false`, `generate_data` to `true`(default length 4e6).

## Training

```bash
source env.sh

python scripts/train.py
```

Currently dataset generation is still pending.
