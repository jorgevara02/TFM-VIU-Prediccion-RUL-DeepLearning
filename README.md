# TFM Experimentación

## Instalación

Requiere [uv](https://docs.astral.sh/uv/).

```bash
uv sync --inexact

# 2. Instalar PyTorch (detecta automáticamente la GPU NVIDIA; si no hay, instala la versión CPU)
uv pip install torch --torch-backend=auto
```

PyTorch no está incluido en `pyproject.toml` para que cada máquina instale el build adecuado (CUDA o CPU).

**Importante:** usar siempre `uv sync --inexact`. Un `uv sync` normal elimina los paquetes que no están en `uv.lock` y desinstalaría PyTorch. Lo mismo ocurre con `uv run`, por lo que conviene usar `uv run --no-sync` o definir la variable de entorno `UV_NO_SYNC=1`. Si PyTorch se desinstala, basta con repetir el paso 2.

Para comprobar que se usa la GPU:

```bash
uv run --no-sync python -c "import torch; print(torch.__version__, torch.cuda.is_available())"
```
