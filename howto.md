1. Start a new repo using `HIRO-template` as the template - don't forget to set to *Private*.

2. Setup secrets and variables under *Settings->Secrets and Variables*:  
`DOCKER_IMAGE_NAME` in Variables  
'HELM_REPO_URL' in Secrets  

4. Clone the repo:
```
git clone https://<token>@github.com/<user>/<repo>.git
```

3. Initialise poetry:
```
poetry config virtualenvs.in-project true
poetry install --no-root --with dev,test
poetry run pre-commit install
```
and run to check
```
poetry run uvicorn app.main:app
```

4. Build the image?
```
echo GHCR_PWD = <token>
echo $GHCR_PWD | nerdctl login -u orestisV-admie --password-stdin ghcr.io
nerdctl image build . -t ghcr.io/orestisv-admie/testimage:latest
nerdctl image push ghcr.io/orestisv-admie/testimage:latest
```
