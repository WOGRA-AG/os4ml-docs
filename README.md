# os4ml-docs
Documentation for [Open space 4 Machine Learning](https://github.com/WOGRA-AG/Os4ML).  
This project is built using [mkdocs](https://www.mkdocs.org).
## Workflow
Clone Repository and navigate to folder

### Install mkdocs
`pip install mkdocs`

### Adding pages
Create a new file with the content of the new page  
`touch docs/xxx.md`  
and add it to the `nav` section of the `mkdocs.yml` file.
```yaml
site_name: Ms4ML
site_url: https://wogra.github.io/os4ml
repo_url: https://github.com/WOGRA-AG/Os4ML
nav:
  - Home: index.md
  - Getting Started: microk8s.md
```

### Build site
`mkdocs build`

### Deploy on git
`mkdocs gh-deploy`
