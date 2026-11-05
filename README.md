# homebrew-krca

Tap de Homebrew para [KRCA - Kubernetes Resource Container Audit](https://github.com/upszot/kubectl-resource-container-audit).

## Instalación

```bash
brew install upszot/krca/krca
```

O, si preferís agregar el tap primero:

```bash
brew tap upszot/krca
brew install krca
```

## Verificación

```bash
krca --version
kubectl-krca --version
kubectl krca --help
```

## Actualización

```bash
brew update
brew upgrade krca
```

## Desinstalación

```bash
brew uninstall krca
brew untap upszot/krca
```

## Requisitos

- `python@3.12` (lo instala Homebrew como dependencia)
- `kubectl` configurado con acceso a un cluster
- `metrics-server` en el cluster para métricas en vivo
- Opcional: Prometheus para el análisis histórico (`--history`)
- Opcional: `wkhtmltopdf` para exportar a PDF

La fórmula instala `krca` y `kubectl-krca`, e incluye los assets CSS/JS necesarios
para exportar HTML/PDF.

## Actualizar la fórmula

La fuente de verdad del paquete es [PyPI](https://pypi.org/project/krca/).
Para una nueva versión:

```bash
# Obtener URL y sha256 del sdist
curl -s https://pypi.org/pypi/krca/json \
  | jq -r '.urls[] | select(.packagetype=="sdist") | "\(.url)\n\(.digests.sha256)"'

# Editar Formula/krca.rb con la nueva url/sha256 y regenerar recursos
brew update-python-resources Formula/krca.rb

# Validar
brew style Formula/krca.rb
brew audit --strict --online upszot/krca/krca
brew install --build-from-source ./Formula/krca.rb
brew test krca
```

Luego commit y push a este repositorio.
