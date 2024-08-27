# `uv==0.3.5` regression

Minimum reproducible example for a regression introduced in `uv==0.3.5` where changes to `pyproject.toml` are not apparently respected.

```console
$ conda create -n regression python=3.10 -y
$ conda activate regression
$ pip install uv==0.3.5
$ uv pip install -e .
  × No solution found when resolving dependencies:
  ╰─▶ Because torchvision==0.19.0 depends on torch==2.4.0 and uv-regression==0.0.0 depends on torch==2.3.1, we can conclude that torchvision==0.19.0 and uv-regression==0.0.0
      are incompatible.
      And because uv-regression==0.0.0 depends on torchvision==0.19.0, we can conclude that uv-regression==0.0.0 cannot be used.
      And because only uv-regression==0.0.0 is available and you require uv-regression, we can conclude that your requirements are unsatisfiable.
```

Solve the unsatisfiability by downgrading `torchvision` to `0.18.1`.

```console
$ uv pip install -e .
  × No solution found when resolving dependencies:
  ╰─▶ Because torchvision==0.19.0 depends on torch==2.4.0 and uv-regression==0.0.0 depends on torch==2.3.1, we can conclude that torchvision==0.19.0 and uv-regression==0.0.0
      are incompatible.
      And because uv-regression==0.0.0 depends on torchvision==0.19.0, we can conclude that uv-regression==0.0.0 cannot be used.
      And because only uv-regression==0.0.0 is available and you require uv-regression, we can conclude that your requirements are unsatisfiable.
```

The same failure, despite the change to `pyproject.toml`. Try downgrading `uv` to `0.3.4`.

```console
$ pip install uv==0.3.4
$ uv pip install -e .
Resolved 13 packages in 866ms
   Built uv-regression @ file:///Users/ringo/Repositories/uv-0.3.5-regression
Prepared 1 package in 588ms
Installed 13 packages in 508ms
 + filelock==3.15.4
 + fsspec==2024.6.1
 + jinja2==3.1.4
 + markupsafe==2.1.5
 + mpmath==1.3.0
 + networkx==3.3
 + numpy==2.1.0
 + pillow==10.4.0
 + sympy==1.13.2
 + torch==2.3.1
 + torchvision==0.18.1
 + typing-extensions==4.12.2
 + uv-regression==0.0.0 (from file:///Users/ringo/Repositories/uv-0.3.5-regression)
```
