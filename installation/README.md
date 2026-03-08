# Collecting Digital Data: The Role of Web-scraping and APIs

## Option 1: Using Google Colab (recommended)

For this course we recommend using [Google Colab](https://colab.research.google.com/), which allows you to run Jupyter Notebooks in your browser without installing anything. You just need a [Google account](https://support.google.com/accounts/answer/27441?hl=en).

**Getting started with Colab:**
1. Go to [colab.research.google.com](https://colab.research.google.com/)
2. Sign in with your Google account
3. Open a notebook using the "Open in Colab" badges in the course README
4. For R notebooks: go to **Runtime > Change runtime type** and select **R**
5. You're ready to go — all Python packages are pre-installed

### Python packages (pre-installed in Colab)

* `requests` - for making HTTP requests
* `beautifulsoup4` - for parsing HTML
* `pandas` - for data manipulation
* `matplotlib` - for visualisation
* `json` - for working with JSON data (part of Python standard library)

### R packages

If you are using the R notebooks, you will need to install the following packages (a code cell at the top of each R notebook handles this for you in Colab):
* `httr` - for making HTTP requests
* `rvest` - for parsing HTML
* `jsonlite` - for working with JSON data
* `dplyr` - for data manipulation
* `ggplot2` - for visualisation

---

## Option 2: Running locally on your own machine

If you prefer to work on your own computer (e.g., for use after the course), follow the step-by-step instructions below.

### Installing Python

**Windows:**
1. Download the latest Python installer from [python.org/downloads](https://www.python.org/downloads/)
2. **Important:** During installation, tick the box that says **"Add Python to PATH"**
3. Click "Install Now" and wait for the installation to complete
4. Verify the installation by opening **Command Prompt** (search for `cmd`) and typing:
   ```
   python --version
   ```
   You should see something like `Python 3.12.x`

**macOS:**
1. Download the macOS installer from [python.org/downloads/macos](https://www.python.org/downloads/macos/)
2. Open the downloaded `.pkg` file and follow the prompts
3. Verify by opening **Terminal** and typing:
   ```
   python3 --version
   ```

**Linux:**
Python is usually pre-installed. Check with `python3 --version`. If not installed, use your package manager (e.g., `sudo apt install python3 python3-pip` on Ubuntu/Debian).

### Installing Python packages

Once Python is installed, open your terminal (Command Prompt on Windows, Terminal on macOS/Linux) and run:

```
pip install requests beautifulsoup4 pandas matplotlib jupyterlab
```

### Installing R and RStudio

1. Download and install R from [cran.r-project.org](https://cran.r-project.org/) — choose the version for your operating system
2. Download and install RStudio Desktop (free) from [posit.co/download/rstudio-desktop](https://posit.co/download/rstudio-desktop/)
3. Open RStudio and install the required packages by running in the R console:
   ```r
   install.packages(c("httr", "rvest", "jsonlite", "dplyr", "ggplot2"))
   ```

### Running Jupyter Notebooks locally

**For Python notebooks:**
1. Open your terminal and type:
   ```
   pip install jupyterlab
   ```
2. Navigate to the folder containing the course notebooks:
   ```
   cd path/to/collecting-digital-data/code
   ```
3. Launch Jupyter Lab:
   ```
   jupyter lab
   ```
4. Your browser will open with the Jupyter interface — click on a notebook file to open it

**For R notebooks in Jupyter:**
1. Open R (or RStudio) and install the IRkernel:
   ```r
   install.packages('IRkernel')
   IRkernel::installspec()
   ```
2. Launch Jupyter Lab from your terminal (`jupyter lab`) — R will now appear as a kernel option
3. Alternatively, you can open the R notebooks directly in RStudio (File > Open File)

### Troubleshooting

| Problem | Solution |
|---------|----------|
| `python` command not found (Windows) | Re-run the Python installer and tick "Add Python to PATH" |
| `pip` command not found | Try `python -m pip install ...` instead |
| `jupyter` command not found | Try `python -m jupyter lab` instead |
| Package installation fails | Try running your terminal as administrator (Windows) or with `sudo` (macOS/Linux) |
| R notebooks won't open in Jupyter | Make sure you ran `IRkernel::installspec()` from within R |
