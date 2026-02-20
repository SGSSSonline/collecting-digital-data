# Collecting Digital Data: The Role of Web-scraping and APIs

## Installing Python

If you would like to download and install Python on your own machine:
* [How to Install Python on Windows 10](https://www.digitalocean.com/community/tutorials/install-python-windows-10)
* The above guide is relevant for installing on Mac also, just make sure you download the Mac version of Python: [https://www.python.org/downloads/macos/](https://www.python.org/downloads/macos/)

## Installing R

If you would like to download and install R on your own machine:
* Download R from [https://cran.r-project.org/](https://cran.r-project.org/)
* Download RStudio (a user-friendly interface for R) from [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)

## Running Jupyter Notebooks

You can run Jupyter Notebooks after installing Python by opening your command prompt and typing `jupyter lab`.

If it isn't installed on your machine yet then type `pip install jupyterlab` into your command prompt first and then type `jupyter lab`.

To run R in Jupyter Notebooks, you will need to install the IRkernel package. Open R and run:

```r
install.packages('IRkernel')
IRkernel::installspec()
```

## Using Google Colab (recommended)

For this course we recommend using [Google Colab](https://colab.research.google.com/), which allows you to run Jupyter Notebooks in your browser without installing anything. You just need a [Google account](https://support.google.com/accounts/answer/27441?hl=en).

### Python packages

The following Python packages are used in this course and are pre-installed in Google Colab:
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
