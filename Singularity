Bootstrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/$basearch/
Include: yum

%help

%setup

%files

%labels

%environment
    export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

%post
    echo "Installing Development Tools YUM group"
    yum -y groupinstall "Development Tools"
    echo "Installing OpenMPI into container..."
    yum -y install wget
    OPENMPI_VERSION=3.1.3
    OPENMPI_NAME=openmpi-${OPENMPI_VERSION}
    wget https://download.open-mpi.org/release/open-mpi/v3.1/${OPENMPI_NAME}.tar.gz
    tar -xvf ${OPENMPI_NAME}.tar.gz
    cd ${OPENMPI_NAME}
    ./configure --prefix=/usr/local
    make all install

#osu bench
     OSU_VERSION=5.4.2
     wget http://mvapich.cse.ohio-state.edu/download/mvapich/osu-micro-benchmarks-${OSU_VERSION}.tar.gz
     tar -xvf osu-micro-benchmarks-${OSU_VERSION}.tar.gz
     cd osu-micro-benchmarks-${OSU_VERSION}
     ./configure --prefix=/usr/local CC=/usr/local/bin/mpicc CXX=/usr/local/bin/mpicxx
     make
     make install

%runscript
    /usr/local/libexec/osu-micro-benchmarks/mpi/pt2pt/osu_bw
    /usr/local/libexec/osu-micro-benchmarks/mpi/pt2pt/osu_latency
