## Public Helm Repo

**If needed**, create a public repo for the helm charts.  
Create a `gh-pages` branch, and set Pages to point to it.

## Private FastAPI Repo

1. Start a new repo using `HIRO-template` as the template - don't forget to set to *Private*.

2. Setup secrets and variables under *Settings->Secrets and Variables*:   
`HELM_TOKEN` in Secrets - store a token that has write access to helm repo  
`DOCKER_IMAGE_NAME` in Variables - set to `<user>/<repo name>`  WARNING: convert both user and repo name to all-lowercase!  
`HELM_REPO` in Variables - set to `<helm_repo_name>`

3. The build of the initial commit will fail, since the necessary secrets/variables are not set.  
If necessary re-run it from the Actions tab on github.


## Manually Build

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

3. Build and push the image
```
export GHCR_PWD = <token>
echo $GHCR_PWD | nerdctl login -u <github_user> --password-stdin ghcr.io
nerdctl image build . -t ghcr.io/<github_user>/<image_name>:<tag>
nerdctl image push ghcr.io/<github_user>/<image_name>:<tag>
```

## Manually Deploy from ghcr

```
export GHCR_PWD = <token>
echo $GHCR_PWD | nerdctl login -u <github_user> --password-stdin ghcr.io
nerdctl run -p 8080:80 <image_url>
```
and check that it runs:
```
curl http://localahost:8080
```
