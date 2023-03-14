# Easiest Way to Configure GitHub Actions to Upload Python Package to PyPI
Uploading your Python package to PyPI can be a tedious task. However, you can automate the process by configuring GitHub Actions. With GitHub Actions, you can create workflows that will automatically build and upload your Python package to PyPI when you push a commit with a tag. Here's how you can set it up:

## Prerequisites
- A Python package to upload
- A GitHub account
- A PyPI account
- A PyPI API token

## Steps
1. Create your desired package.

2. Upload your package to GitHub.

3. Open your repository on GitHub and click on Actions.

4. Click on "New Workflow" and select "Publish Python Package".

5. A new YAML file will get created inside the .github/workflows folder.

Delete all the contents of the YAML file and copy and paste the following content:
```
name: Upload Python Package

on:
  push:
    tags:
    - '*'

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v2
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install setuptools wheel twine
    - name: Build and publish
      env:
        TWINE_USERNAME: __token__
        TWINE_PASSWORD: ${{ secrets.TEST_PYPI_API_TOKEN }}
      run: |
        python setup.py sdist bdist_wheel
        twine upload --repository testpypi dist/* --skip-existing


```
7. Commit the changes.

8. The push would start only when you push a commit with a tag. To create a tag, use the following command: ```git tag <tag_name>```

9. In the YAML file, replace ${{ secrets.TEST_PYPI_API_TOKEN }} with the name of the PyPI API token you saved in the repository's secrets..

10. To create a PyPI API token, navigate to your PyPI account's settings and create a new token. Save the token's value as a secret in your repository's settings.

11. Use this in TWINE_PASSWORD, and don't forget to add variable formatting.

## Contributing
Contributions are always welcome! If you have suggestions or improvements to make, please create a pull request
Please make sure to update tests as appropriate.


