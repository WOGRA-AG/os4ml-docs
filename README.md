# os4ml-docs
Documentation for [Open space 4 Machine Learning](https://github.com/WOGRA-AG/Os4ML).  
This project is built using [mkdocs](https://www.mkdocs.org). This is a test.
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
  - Xxx: xxx.md
```

### Test site locally
`mkdocs serve`  
and open a browser of your choice on `http://127.0.0.1:8000/os4ml/`

### Deploy
To release a new Page, just push the new corresponding branch to the repository and create a merge request on the main branch.  
The CI/CD Pipeline will autmatically build and deploy the new page, if the merge request gets accepted.
