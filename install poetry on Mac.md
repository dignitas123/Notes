# install poetry using brew
brew install poetry

# check if installed correctly, eventually add export PATH="$HOME/.poetry/bin:$PATH" to /etc/zprofile and /etc/zshrc
poetry --version

# create conda env to install, with pyhthon version
conda --create myEnv python=3.8
conda activate myEnv

# install the project inside the environment
poetry install

# build the distribution files
poetry build

# configuration for test.pypi
poetry config repositories.test-pypi https://test.pypi.org/legacy/

# create api token in testp.pypi account and copy secret
poetry config pypi-token.test-pypi <secret>

# publish
poetry publish -v -r test-pypi
