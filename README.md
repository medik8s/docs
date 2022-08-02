# Medik8s
![medik8s logo](images/medik8s-logo.png "Medik8s Logo")

Documentation for the medik8s collection of projects

## Preview

To preview the page locally, run

```shell
export JEKYLL_VERSION=3.8
docker run --rm \
  --volume="$PWD:/srv/jekyll:Z" \
  -p 4000:4000 \
  -it jekyll/builder:$JEKYLL_VERSION \
  bash -c "bundle && jekyll serve"
```

and open `http://127.0.0.1:4000/` in your browser.

### Troubleshooting
- make sure command is executed in `docs` folder.
- make sure `_site` dir exists.
  - if it doesn't in order to create it run: `mkdir _site && chmod -R 777 _site`
  