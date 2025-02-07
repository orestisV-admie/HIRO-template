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
