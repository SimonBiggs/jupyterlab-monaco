# JupyterLab Monaco Editor Extension

A JupyterLab extension providing the [Monaco](https://github.com/Microsoft/monaco-editor/) editor.

## Prerequisites

* JupyterLab 0.32
* The modifications at https://github.com/jupyterlab/jupyterlab/issues/4406 must be applied to the JupyterLab webpack config (usually in the `site-packages/jupyterlab/staging/webpack.config.js`)

## Development

For a development install, do the following in the repository directory:

```bash
yarn install
yarn run build
jupyter labextension link .
```

To rebuild the package and the JupyterLab app:

```bash
yarn run build
jupyter lab build
```

## Development notes

The tricky thing about this repo is that we webpack up Monaco as part of the build process and publish those JavaScript files as part of the package. Because Monaco likes to use web workers to start up parts of the application, we must have standalone js files and a way to get the URL for those files in the final JupyterLab build. We get the URL in the extension by using the webpack file loader in the JupyterLab build for the Monaco js files (JLab knows to use the file loader because we prefix the filename with `JUPYTERLAB_FILE_LOADER_`).

