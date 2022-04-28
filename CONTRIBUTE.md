# Publish
Embed-Markdown is distributed through `pip`. To gain access to this project,
contact project maintainer [here](https://pypi.org/project/embed-markdown/).

To publish this package, you must:
1. Have an PyPI account
2. Create an API key following [these steps](https://packaging.python.org/en/latest/tutorials/packaging-projects/#uploading-the-distribution-archives)
   1. Don't exit the page until you confirm the API key works
   2. Follow instructions listed in the API token page to configure ~/.pypirc
3. Follow [these steps](https://packaging.python.org/en/latest/tutorials/packaging-projects/#uploading-the-distribution-archives) to publish the package:
   1. Run `python3 -m build` to create a archive
   2. Run `python3 -m twine upload dist/*` to upload the archive to PyPI
   3. Run `pip install --upgrade embed-markdown` to verify the distribution
