In `pyproject.toml':
```
[tool.poetry]
name = "template-python"
version = "0.0.0"
description = "Test Web service."
readme = "README.md"
authors = ["Orestis Vantzos <o.vantzos@admie.gr>"]
license = "MIT"
repository = "https://github.com/orestisV-admie/HIRO-template"
homepage = "https://github.com/orestisV-admie/HIRO-template"
packages = [{include = "*", from="app"}]

[tool.poetry.dependencies]
python = "^3.10"
```

```
poetry config virtualenvs.in-project true
poetry install --no-root --with dev,test
poetry run pre-commit install
poetry run uvicorn app.main:app
```

```
echo GHCR_PWD = <token>
echo $GHCR_PWD | nerctl login -u orestisV-admie --password-stdin ghcr.io
nerdctl image build . -t ghcr.io/orestisv-admie/testimage:latest
nerdctl image push ghcr.io/orestisv-admie/testimage:latest
```
