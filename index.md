
# Easiest Way to configure GITHUB Actions To Upload Python Package to PypI  

## Authors

- [@LpCodes](https://github.com/LpCodes)


## Steps

1. Create your desired package
2. Upload to GitHub
3. Open your repository on GitHub & Click on Actions
4. Select New Workflow
5. Select Publish Python Package
6. A new yml file will get created inside workflows folder
7. Delete All the contents & Copy paste the below content & commit
8. The push would start only when u push a commit with tag

    
        name: Upload Python Package
        
        on:
          push:
            tags:
            - '*'
        jobs:
          deploy:
            runs-on: ubuntu-20.04
        
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
    
## Contributing

Contributions are always welcome! Help to Improve the doc 




