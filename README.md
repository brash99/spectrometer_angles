# Spectrometer Angles

## Quick start

### Extracting images from coda files with `extract_coda_images`

```
./bin/extract_coda_images raw/coin_all_03547.dat -r 3547
SHMS_angle_3547.jpg
HMS_angle_3547.jpg
```

```
./bin/extract_coda_images -h
USAGE: extract_coda_images [-r] [-p] [-h] DAT-FILE
  
  DESCRIPTION:
          ./extract_coda_images extracts the spectrometer camers angles from the raw coda files.
  
  ARGUMENTS: 
          DAT-FILE           CODA file (e.g. raw/coin_all_01234.dat)
  OPTIONS: 
          -r,--run <number>  Run Number (default:0) is currently only used for output file name.
          -t,--tag <tag>     File tag is appended to the output file name : shms_angle_0_<tag>.jpg
          -p,--png           Convert the output Output a png file instead
          -d,--debug         Debug printing
          -h,--help          Print this help
  
 Please report bugs to Whitney Armstrong <whit@jlab.org>
```

### Comparing angle images: `compare_images`

Test images:

* `test_images/angle_test1.jpg` SHMS camera
* `test_images/angle_test2.jpg` Same as previous but shifted a few pixels
* `test_images/angle_test3.jpg` Different run  but same SHMS angle
* `test_images/angle_test4.jpg` Very different SHMS angle setting angle

#### Test 1

![t1](test_images/angle_test1.jpg)

![t2](test_images/angle_test2.jpg)

The second image above is the same as the first but has the floor markings 
slight shifted to the left. This emulates a small shift in the rotation after 
initial angle setting.


step-1a:

![test12_step1](test_images/test_1-2/test1.png)

step-1b:

![test12_step2](test_images/test_1-2/test2.png)

step-2: take a difference

![test12_step1](test_images/test_1-2/test3.png)

step-3: re-process the difference 

![test12_step2](test_images/test_1-2/test4.png)

```
./bin/compare_images test_images/angle_test1.jpg test_images/angle_test2.jpg -d
4231
```
Note that a non-zero values indicate significant differences. This value is  is 
a count of the number of blueish pixels.

#### Test 2

![t1](test_images/angle_test1.jpg)

![t2](test_images/angle_test3.jpg)

The second image is the exact same setting just at a different time.  
Comparison should yield no differences.


step-1a:

![test13_step1](test_images/test_1-3/test1.png)

step-1b:

![test13_step2](test_images/test_1-3/test2.png)

step-2: take a difference

![test13_step1](test_images/test_1-3/test3.png)

step-3: re-process the difference 

![test13_step2](test_images/test_1-3/test4.png)

```
./bin/compare_images test_images/angle_test1.jpg test_images/angle_test3.jpg
0
```

Note that a non-zero values indicate significant differences. This value is  is 
a count of the number of blueish pixels.

#### Test 3

![t1](test_images/angle_test1.jpg)

![t2](test_images/angle_test4.jpg)

The second image is a very different setting. Let see what happens

step-1a:

![test14_step1](test_images/test_1-4/test1.png)

step-1b:

![test14_step2](test_images/test_1-4/test2.png)

step-2: take a difference

![test14_step1](test_images/test_1-4/test3.png)

step-3: re-process the difference 

![test14_step2](test_images/test_1-4/test4.png)

```
./bin/compare_images test_images/angle_test1.jpg test_images/angle_test4.jpg
10815
```

There is a lot of the blue color as measured by the return value.
The returned value is a count of the number of blueish pixels.

**Todo**: 

- Add more tests and examples.
- Add test with HMS images


##  Ideas

**Currently not functional**

Todo:

1. Define standard image processing
2. Find angle number in image
3. Find (x,y) coordinate and size.
4. Determine number value (OCR or other method)
5. Calculate lookup of [number+coordanate] -> precise angle


## Progress

This should print out 14
```
./get_spectrometer_angle -r 3566  -d test  # should print 14
./get_spectrometer_angle -r 3293  -d test  # doesn't work yet
```





