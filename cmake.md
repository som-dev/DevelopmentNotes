# CMake

## Common Build Types
* Release
* Debug
* RelWithDebInfo

## Setup
```
# from folder containing CMakeLists.txt:

# generate build files:
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=<BuildType> ../

# perform the build:
cmake --build ./
```

## Script for building multiple build types
```
echo Building All...
types=( Release RelWithDebInfo Debug )
for i in "${types[@]}"
do
	echo Building $i...
	mkdir -p ./build/$i
	cd ./build/$i
	cmake -DCMAKE_BUILD_TYPE=$i ../../
	cmake --build ./
	cd -
done
echo Done Building All
```
