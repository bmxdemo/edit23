# Edit School 2023

This repository sets up the exercise for the Edit School 2023.
The data exercise requires two pieces:
 * a docker image with a working environment
 * actual data

# Getting started

This assumes you are working in a linux environment. The same should be executable also in a windows or Mac OSX environments.
Prerequisites:
 * You need docker downloaded. All the other dependencies live in the image
 * You need sufficient free space on your hard drive. BMX data are big: 28G per day.

Steps:
1. Download the relevant docker image:
```
docker pull slosar/edit23
```

2. Create a directory and download some data from [https://www.cosmo.bnl.gov/www/bmx/edit2023/](https://www.cosmo.bnl.gov/www/bmx/edit2023/).

You want to do something like:

```
cd ~
mkdir bmx; cd bmx
mkdir data; cd data
wget https://www.cosmo.bnl.gov/www/bmx/edit2023/edit_230924_2200.tgz
tar zxvf edit_230924_2200.tgz && rm edit_230924_2200.tgz
cd ..
```

3. Pull this repository

```
git clone https://github.com/bmxdemo/edit23.git
cd edit23
```

4. Run the docker image, pointing the data to the right place:

```
docker run -p 2023:2023 -v $HOME/bmx/data:/bmxdata -v $PWD:$PWD -w$PWD --user $(id -u):$(id -g)  slosar/edit23
```
Different pieces do the following:
 * `-p 2023:2023` maps port 2023 running inside the container: we have jupyter lab running on this port
 * `-v $HOME/bmx/data:/bmxdata` makes the data downloaded under point 2 above appear in `/bmxdata` inside the container
 * `-v $PWD:$PWD` makes your current directory appear inside the container
 * `-w $PWD` makes the above directory the current directory where jupyter lab lives
 * `--user $(id -u):$(id -g)` makes this container run as a current user, as a basic safety precaution

5. Run the jupyter notebook. Open your browser and go to [http://localhost:2023](http://localhost:2023). Jupyter should open.
   Open `example.ipynb` and try to run it to confirm basic functionality.
   



