Pin to earlier Python version
```zsh
uv python pin 3.11
```

In pyproject.toml, add these entries to the existing [tool.uv] section:
```
[tool.uv]
required-environments = [
    "sys_platform == 'darwin' and platform_machine == 'x86_64'",
]
constraint-dependencies = [
    "onnxruntime<=1.23.2; sys_platform == 'darwin' and platform_machine == 'x86_64'",
]
```
Then rebuild the lock and environment:
```zsh
uv lock --upgrade-package onnxruntime
uv sync
```

Confirm the resolved version:
```zsh
uv run python -c "import platform, onnxruntime; print(platform.machine(), onnxruntime.__version__)"
```