---
title: "What Kisii Is Listening To At Night"
date: 2020-03-08T21:59:03+03:00
draft: false
---

The title of this post might not reflect the concept behind this project but nevertheless just
read along.

The Electromagnetic spectrum (Spectrum of Electromagnetic Radiation) is one massive real eastate 
that is hardly seen by the naked eye. Only a small part of it is visible light while the rest is 
out of our eyes reach.

Tonight I sought to see what FM frequencies are in use in Kisii County on this cold Sunday night.

## Requirements:

* [rtl_power](http://kmkeen.com/rtl-power/2014-07-27-08-09-20-103.html)
* [python3](https://python.org)
* [heatmap.py](https://github.com/keenerd)


rtl_power, created by kmkeen is a program that does band scanning. Its unique features as per the developers site include:

* Unlimited frequency range. You can do the whole 1.7GHz of a dongle.
* Unlimited time. At least until you run out of disk for logging.
* Unlimited FFT bins. But in practice I don't think I've taken it above 100k bins.
* Quantitative rendering. Exact power levels are logged.
* Runs on anything. A slower computer will use less samples to keep up.

Tonight am doing a scan on FM from 88Mhz-108Mhz. The command to do so is:

```
rtl_power -f 88M:108M:8k -g 50 -i 10 -e 2h fm2_band.csv
```
This will produce a large CSV file which contains the signals which have been discovered.

Where:

* -f:
* 88M:108M is the frequency range
* 8k: 
* 50:
* -i:
* 10:
* -e:
* 2h: Duration of scan in hours
* fm2_band.csv: Output File name for the CSV file

Once the scan has been complete, the CSV file might be large depending on the scan duration. Run the following command to produce a graphical
output.

```
python heatmap.py fm2_band.csv map2.png
```
The output shall be a PNG file which shows a survey of the whole band. See below:

![band](/img/ham/fm.png)

This image is really wide so scroll sideways to see the whole frequency width.

## Analysis

From the above image we can see that in Kisii County you can get upto 10 clear FM Signals or stations. 
The rest will be heard but not so clear. At the moment I cant know which stations but from the scale at 
the top of the image, you can read out the frequency and look it up against this post to know which station that is.

Back to DXing :-]
