# Python

## Install / Setup
```bash
# check what version is installed
python3 -V

# install pip
sudo apt install -y python3-pip

# install a pip package
pip3 install package_name

# install a python library manually (no pip)
# after cloning the repository, go to where setup.py is located
python3 setup.py install

```

## Array manipulation
```python

# loop through all items of array
array = ['one', 'two', 'three']
for x in array:
	print(x)

```

## Date and time
```python
# get current datetime
now = datetime.now()
print(now.strftime("%d/%m/%Y %H:%M:%S"))

```