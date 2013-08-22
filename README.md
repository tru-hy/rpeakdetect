# ECG beat detection

Implements an ECG beat (acutally R-peak/QRS-complex) detection
algorithm based on the article [An Efficient R-peak Detection Based on New Nonlinear Transformation and First-Order Gaussian Differentiator](http://link.springer.com/article/10.1007/s13239-011-0065-3/fulltext.html) with some tweaks.


## Requirements

NumPy and SciPy and matplotlib if you want to use the plotting.

## Usage

The module can be run from command line. Reads newline-delimited raw
ECG sample values and takes the sampling rate in Hz as an argument. In
default mode outputs the detected peak sample numbers in the same format. Eg:

    python2 rpeakdetect.py 128 < ecg_data.csv > beat_samples.csv

With added argument `plot` plots the detection.

    python2 rpeakdetect.py 128 < ecg_data.csv

Running the latter with some [sample data](https://raw.github.com/tru-hy/rpeakdetect/gh-pages/ecg_sample.csv)
produces something like the image below.
(The recording is from mobile setting with a rather unconventional
electrode placment, hence the noisiness and a bit weird ECG waveform.)

Also note that despite the name, the algorithm doesn't actually detect
the R-peaks themselves. Rather the detected time is better described as
"midpoint of the QRS complex". Further the implementation may cause an artificial
shifting of a few (1-2) samples due to not compensating the signal shifting during
taking differences. If you need/want to detect the exact R-peak,
it's quite straightforward to find by locating the maximum signal value
in a small (some milliseconds) window around the detected position.

![Detection result example](https://raw.github.com/tru-hy/rpeakdetect/gh-pages/rpeakdetect_sample.png)
