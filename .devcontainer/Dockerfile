# Pre-built Dev Container Image for R. More info: https://github.com/rocker-org/devcontainer-images/pkgs/container/devcontainer%2Ftidyverse
# Available R version: 4, 4.1, 4.0
ARG VARIANT="4.2"
FROM ghcr.io/rocker-org/devcontainer/tidyverse:${VARIANT}

# Install system dependencies needed for most R packages and for pak to work correctly
RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends \
    git \
    libcurl4-openssl-dev \
    libssl-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install the 'pak' package from its dedicated repository and use it to install 'smdi'
# Combining these steps into a single RUN command ensures the R session context is consistent.
RUN R -e "install.packages('pak', repos = 'https://r-lib.github.io/p/pak/stable/')" && \
    Rscript -e "pak::pak('smdi')"

# Copy RStudio preferences
COPY rstudio-prefs.json /rstudio-prefs.json
COPY copy-rstudio-prefs.sh /copy-rstudio-prefs.sh
RUN chmod +x /copy-rstudio-prefs.sh