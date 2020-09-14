# Statistics Library (version: 1.0)

> &copy; 2012-2013 Scott Daniels <provideyourown.com>
> under GNU General Public License

The Statistics Library permits you to easily perform statistical analysis 
on data collected. This information can be useful for determining data
quality as well as smoothing jittery readings such as those from touch
sensors.

In order to conserve precious SRAM when necessary, two versions of the
library are available:

IntStatistics.h - uses only integer math
Statistics.h - uses floating point math

The inclusion of floating point math in an Arduino sketch will consume
over 200 bytes of SRAM in overhead.

## Methods


**Construction & Configuration**

```C++
// specify the number of samples to be collected
Statistics(numSamples)

// change the sample size (will reset any data collected)
void setNewSampleSize(numSamples)

// reset the collected data
void reset()
```
**Adding data**

```C++
// add a data point to the collection
void addData(val)
```

**Data Analysis**

```C++
// the arthemetic mean of the data collected
Type mean()

// the variance of the data
Type variance()

// the standard deviation 
// !! NOT available in the integer version !!
Type stdDeviation()

// the maximum data point
Type maxVal()

// the minimum data point
Type minVal()
```

## Usage example

```C++
#include <Statistics.h>

Statistics stats(10);

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  int data = analogRead(A0);
  stats.addData(data);
  
  Serial.print("Mean: ");
  Serial.print(stats.mean());
  Serial.print(" Std Dev: ");
  Serial.println(stats.stdDeviation());
}
```
