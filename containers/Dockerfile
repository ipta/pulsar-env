FROM mambaorg/micromamba
RUN micromamba install --yes --name base\
  -c conda-forge\
  -c defaults\
  -c demorest\
  python=3.9\
  pip\
  mkl\
  jupyter\
  ca-certificates\
  certifi\
  openssl\
  libblas[build=*mkl]\
  tempo2\
  matplotlib\
  astropy\
  bokeh\
  bottleneck\
  dask\
  h5py\
  imagecodecs\
  imageio\
  ipympl\
  numba\
  numexpr\
  pandas\
  patsy\
  pyerfa\
  pytables\
  pywavelets\
  scikit-image\
  scikit-learn\
  scikit-sparse\
  scipy\
  seaborn\
  seaborn-base\
  statsmodels\
  tifffile\
  vincent\
  yt\
  gmp\
  mpfr\
  nose\
  suitesparse\
  ptmcmcsampler\
  wand\
  marshmallow\
  cython\
  healpy\
  jplephem\
  ephem\
  corner\
  pyyaml\
  ruamel.yaml\
  pytest\
  docutils\
  pytest-xdist\
  psrchive\
  psrqpy\
  libstempo\
  pint-pulsar>=0.9\
  mpi4py\
  enterprise-pulsar\
  enterprise_outliers\
  enterprise_extensions\
  astroquery\
  pandas\
  pgplot\
  pint-pal>=0.1.0\
  pymultinest>=2.11\
  acor>=1.1.1\
  pypulse>=0.1.1\
  gitpython

RUN micromamba clean --all --yes

ARG MAMBA_DOCKERFILE_ACTIVATE=1

RUN pip install --no-cache git+https://github.com/pennucci/PulsePortraiture.git@py3
