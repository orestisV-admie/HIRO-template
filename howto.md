## Public Helm Repo

**If needed**, create a public repo for the helm charts.  
Create a `gh-pages` branch, and set Pages to point to it.

## Private FastAPI Repo

1. Start a new repo using `HIRO-template` as the template - don't forget to set to *Private*.

2. Setup secrets and variables under *Settings->Secrets and Variables*:   
`HELM_TOKEN` in Secrets - store a token that has write access to helm repo  
`DOCKER_IMAGE_NAME` in Variables - set to `<user>/<repo name>`  
`HELM_REPO` in Variables - set to `<helm_repo_name>`

## Manually Deploy

1. Clone the repo:
```
git clone https://<token>@github.com/<user>/<repo>.git
```

2. Initialise poetry:
```
poetry config virtualenvs.in-project true
poetry install --no-root --with dev,test
poetry run pre-commit install
```
and run to check
```
poetry run uvicorn app.main:app
```

3. Build the image?
```
echo GHCR_PWD = <token>
echo $GHCR_PWD | nerdctl login -u orestisV-admie --password-stdin ghcr.io
nerdctl image build . -t ghcr.io/orestisv-admie/testimage:latest
nerdctl image push ghcr.io/orestisv-admie/testimage:latest
```
