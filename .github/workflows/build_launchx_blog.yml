name: Build Personal Blog
on: push

jobs:
  build:

    name: Build and update website
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
      with:
        submodules: true
        fetch-depth: 0
    - name: Setup GoHugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: '0.92.0'
    - name: Commit Update
      run: |
        echo ":: Eliminando versión previa ::"
        rm -rf docs
    - name: Build drafts
      run: hugo -D
    - name: Commit Update
      run: |
        echo ":: Renombrando nueva version ::"
        mv public/ docs/
        git config --global user.email "launchx@innovaccion.mx"
        git config --global user.name "Launch X Backend Node JS"
        git add .
        git commit -m "GitHub Actions: Build ok"
    - name: Push changes
      uses: ad-m/github-push-action@master
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        branch: ${{ github.ref }}
