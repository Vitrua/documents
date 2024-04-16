## Local test
With the setup procedure in material mkdocs already completed
```
source venv/bin/activate
mkdocs serve
```
## Deploy

Merge to main branch.

If any dependencies has been added since last deploy, you may need to install them in the ci pipeline.

Verify github pages maintained the website 'docs.vitrua.top' and it poits to the branch 'gh-pages'.