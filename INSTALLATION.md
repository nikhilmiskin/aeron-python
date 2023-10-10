# Install Aeron
apt update -y && apt upgrade -y ; \
apt install -y libbsd-dev uuid-dev ca-certificates-java default-jdk curl git ; \
git clone -b 1.42.1 https://github.com/real-logic/aeron.git ; \
cd aeron ; \
./cppbuild/cppbuild --no-system-tests --build-aeron-driver --build-archive-api --package ; \
./cppbuild/Release/aeron-1.42.1-Linux.sh --skip-license --prefix=/usr/local ; \
cd ; \
rm -rf aeron ; \

# Set LD_LIBRARY_PATH env variable
export LD_LIBRARY_PATH="/usr/local/lib"

# Start Aeron media driver
aeronmd -Daeron.print.configuration=true

# Install aeronpy pip package
pip3 install aeronpy@git+https://github.com/nikhilmiskin/aeron-python.git