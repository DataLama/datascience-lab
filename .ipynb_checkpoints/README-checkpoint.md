# Docker for DataScientists.
My docker container for datascience.


## Main features
- Base docker image is [deepo](https://github.com/ufoym/deepo)
- Set **Jupyterlab** and install **jupyterlab extensions**.
- Install **orca** docker container to fully use data visualization package **plotly**.

## Details
### Quickstart
**build docker image**
```bash
sudo docker build --tag datalama/deepo:lab .
```

**docker run**
```bash
sudo docker run -itd -p 8888:8888 -p 6006-6015:6006-6015 --name lab --ipc=host datalama/deepo:lab jupyter lab --no-browser --ip=0.0.0.0 --allow-root --NotebookApp.token= --notebook-dir='/root'
```
- I recommend add your volumes.

**docker exec**
```bash
docker exec -it lab /bin/zsh
```


### [Jupyterlab extension list](https://github.com/topics/jupyterlab-extension?fbclid=IwAR1rMRoJU-PQEng5cJX7aHvUAOF6ifecASC6Tz61unE07kxNbtjIDa4XMiE)

here's my favorites.
- jupyterlab with ipywidgets packages(e.g. tqdm.notebook, plotly)
    - `jupyter-widgets/jupyterlab-manager`
- To visualize plotly on jupyterlab
    - `plotlywidget`, `jupyterlab-plotly`
- draw.io
    - `jupyterlab-drawio `
- R studio style variable inspector
    - `@lckr/jupyterlab_variableinspector `
- table of contents for jupyter lab
    - `@jupyterlab/toc`
- jupyter lab extension for git
    - `@jupyterlab/git`


### Install Jupyterlab extensions by hands
Sometimes, it is hard to build docker images with installing jupyterlab extensions. Then, I recommend install jupyterlab by hands.

- Enable Extension Manager
<img src="images/screen_1.png">

- Click Extension Manager(puzzle icon)
<img src="images/screen_2.png">

- Search, Install and Build !!!
<img src="images/screen_3.png">

### plotly orca setup
If you use plotly to EDA or visualize your data, sometimes you may want to export your figure. At that time, you need the [orca(Electron app)](https://github.com/plotly/orca). Howerver, running orca in your container is a little bit tricky(chromium issue).

I recommend referring to this [notebook]().
