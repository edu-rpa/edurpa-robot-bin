# Build Linux Executable File
Using Go lang to build robot binary for robot EC2  fetch credential from main server
using EC2 enviroment variable


# Build Binary For Multiple Platform
## Using command line
''' bash
GOOS=linux GOARCH=amd64 go build -o get-credential .
'''
## Using Docker
docker run -it --rm \
    -v D:/Thesis/Project/edu-rpa-robot-SDK:/go/src/app \
    -w /go/src/app \
    -e CGO_ENABLED=1 \
    docker.elastic.co/beats-dev/golang-crossbuild:1.18-main\
    --build-cmd "go build -o linux_exe" \
    -p "linux/amd64"

# Upload binary on S3 and robot will fetch on start up
aws s3 cp get-credential s3://edu-rpa-robot/utils/get-credential
