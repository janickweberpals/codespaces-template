# Pre-built Dev Container Image for R. More info: https://github.com/rocker-org/devcontainer-images/pkgs/container/devcontainer%2Ftidyverse
# Available R version: 4, 4.1, 4.0
ARG VARIANT="4.2"
FROM ghcr.io/rocker-org/devcontainer/tidyverse:${VARIANT}

# Install system dependencies for common R packages
RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends \
    git \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    build-essential \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install pak and then smdi using pak
ENV PKG_SYSREQS=false
RUN R -e "install.packages('pak', repos = 'https://r-lib.github.io/p/pak/stable/')" && \
    Rscript -e "pak::pkg_install('smdi')"

# Copy RStudio preferences
COPY rstudio-prefs.json /rstudio-prefs.json
COPY copy-rstudio-prefs.sh /copy-rstudio-prefs.sh
RUN chmod +x /copy-rstudio-prefs.sh
