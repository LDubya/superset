Yeah, setting up a development environment is not as advertised. Docker did not work for me. This is what did:

Here are the steps to set up the Superset development environment from scratch based on our successful setup:

### 1. **Install System Dependencies**

Make sure you have the necessary system dependencies installed. This includes Python, Node.js, and Yarn. You also need to have `pyenv` and `pyenv-virtualenv` for managing Python versions and virtual environments.

```sh
brew install pyenv pyenv-virtualenv
brew install node
brew install yarn
brew install libpq # For PostgreSQL, if you're using it as a database
```

### 2. **Set Up Python Environment**

Use `pyenv` to install the correct Python version with OpenSSL support.

```sh
env PYTHON_CONFIGURE_OPTS="--with-openssl=$(brew --prefix openssl@3)" pyenv install 3.9.13
pyenv virtualenv 3.9.13 superset-env
pyenv activate superset-env
```

### 3. **Clone the Superset Repository**

```sh
git clone https://github.com/apache/superset.git
cd superset
```

### 4. **Install Python Dependencies**

Install the required Python dependencies using `pip`.

```sh
pip install -r requirements.txt
pip install -r superset/translations/requirements.txt
pip install apache-superset
```

### 5. **Set Up Superset Configuration**

Create a configuration file `superset_config.py` and set the necessary configurations, such as `SUPERSET_SECRET_KEY`.

### 6. **Initialize Superset Database**

Create an admin user and upgrade the database.

```sh
superset fab create-admin
superset db upgrade
```

### 7. **Load Examples and Initialize Superset**

Load the example data and initialize Superset.

```sh
superset load_examples
superset init
```

### 8. **Run Superset**

Start the Superset server.

```sh
superset run -p 8088 --with-threads --reload --debugger
```

### Summary of Commands

Here’s a summary of the commands in sequence for easy reference:

```sh
# System dependencies
brew install pyenv pyenv-virtualenv
brew install node
brew install yarn
brew install libpq

# Set up Python environment
env PYTHON_CONFIGURE_OPTS="--with-openssl=$(brew --prefix openssl@3)" pyenv install 3.9.13
pyenv virtualenv 3.9.13 superset-env
pyenv activate superset-env

# Clone Superset repository
git clone https://github.com/apache/superset.git
cd superset

# Install Python dependencies
pip install -r superset/translations/requirements.txt
pip install apache-superset

# Superset configuration (ensure to edit superset_config.py with necessary configs)
# Create superset_config.py and add SUPERSET_SECRET_KEY

# Initialize Superset
superset fab create-admin
superset db upgrade

# Load examples and initialize Superset
superset load_examples
superset init

# Run Superset
superset run -p 8088 --with-threads --reload --debugger
```

By following these steps, you should be able to set up the Superset development environment smoothly.