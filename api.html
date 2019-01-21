`

# QA401 REST API

* * *

# General Operation

* * *

## Philosophy

The original QA401 API was based on Dot Net remoting. This is an exceptionally clean and type-safe interface for sharing data across a wire. But it's not readily replicated outside of DotNet, and it's also been deprecated by Microsoft. REST as a design philosophy has gained enormous momentum, and as such it's achieved generous support and careful consideration on just about every language and platform imaginable.

## Basic Operation

The flow of using the QA401 over a REST interface is straightforward:

1\. Set the operating parameters, such as audio buffer size and windowing types. This is accomplished with multiple PUT operations.

2\. After the desired configuration is achieved, an HTTP POST is issued to start an acquisition. This occurs with the parameters that were specified in step 1.

3\. The user can initiate analysis on the acquired data repetitively until the requirements are met. Note that while you CAN pull over the raw acquired data--either as a time or frequency series--many basic operations, such as computing noise or THD or measuring peak levels can be computed without pulling any raw data from the server.

## Simple Example

As a very simple example, let's look at the HTTP commands you'd use to to make a 1 KHz THD measurement:

First, we'd want to set Audio Generator 1 'on', at a level of 0 dBV and a frequency of 1 KHz. That is accomplished with the following PUT command

HTTP PUT localhost:9401/Settings/AudioGen/1/1/1000/0

Next, we specify we want a 32K FFT buffer size:

HTTP PUT localhost:9401/Settings/BufferSize/32768

Then, we kick off an acquisition using a POST:

HTTP POST localhost:9401/Acquisition

The POST won't return until the acquisition has completed--generally a few hundred milliseconds. When the POST returns, it doesn't bring any data with it. Instead, the JSON response from the POST command will contain a single value, such as:

{"SessionId":"286930"}

All operations will return the same SessionId until the next acquisition is completed. This allows you to ensure the data set you are operating on remains the same.

We can then ask the server to perform a measurement on the acquired data. For example, to measure the THD on the data we just collected, we'd issue a

GET localhost:9401/ThdDb/1000/20000

In response to the above GET, the server would respond

{"SessionId":"286930", "Left":"-101.929476869617", "Right":"-98.8973249362777"}

Note in the above we see the same SessionId as before, indicating this is the same set of data. And we can also see the THD values returned for both the left and right channel. If we issued the command again, we'd see the exact same return string since the data the THD computation is operating upon is unchanged (and indicatedby the same SessionId).

Note that without the SessionId, it would be possible for an errant acquisition to be started by a 3rd party. While the REST interface doesn't contemplate user accounts or security, it does make it possible to ensure the data you are operating upon is the data you expect.

* * *

# Returned Data Types

* * *

Depening on the operation, the server may return one of 6 data types. All are JSON structures.  

## EMPTY

An empty return will consists of a JSON structure that contains a single element, which is the Session ID. This would appears as

{"SessionId":"286930"}

As discussed above, the Session ID for all return types will remain constants across the lifetime of an acquisition.

## BOOLEAN

A boolean return will consists of a JSON structure that contains two elements: a Session ID and a value that was either True or False. This would appears as

{"SessionId":"286930", "Value":"true"}

As discussed above, the Session ID for all return types will remain constants across the lifetime of an acquisition.

## INT

A int return will consists of a JSON structure that contains two elements: a Session ID and a value that is a signed 32-bit int. This would appears as

{"SessionId":"286930", "Value":"13"}

As discussed above, the Session ID for all return types will remain constants across the lifetime of an acquisition.

## SCALAR

A Scalar return will consists of a JSON structure that contains a SessionId and a scaler double value. This would appears as

{"SessionId":"286930", "Value":"3.1415"}

A scalar return type is used when a single double value needs to be returned. An example might be the current software version in use.

## SCALAR PAIR

A Scalar Pair return will consists of a JSON structure that contains a pair of scalar values. This would appears as

{"SessionId":"286930", "Left":"-101.929476869617", "Right":"-98.8973249362777"}

This return type is useful for returning a left/right pair of measurements. For example, if you asked for the THD to be computed on some acquired data, both the left and right data would be returned. If you are only interested in a single channel, then just ignore the un-needed channel.

## DOUBLE ARRAY

A Double Array return will consists of a JSON structure that contains a Session Id, an element named Dx, and two MIME-encoded strings: One for the left channel, and one for the right channel. This would appears as

{"SessionId":"286930", "Dx":"5.859375", "Left":"PElx+QYE", "Right":"Or9Ub8kU" }

The Dx value represents the spacing of the array data. The MIME-encoded strings represent binary data for the left and right channels. While the return strings above are short for demonstration, in actuality the real strings will be very long--several megabytes in some cases. To decode this data, you need to use the standard functions in your preferred language to convert mime strings to byte arrays, and then assemble those byte arrays into 64-bit doubles. Once you have reconstructed the arrays of doubles, the Dx value tells you the spacing between each value. For example, the above data in the example is frequency bin data, and the spacing between each bin is 5.85 Hz. But you could also pull over the time-domaindata too. In that case, the Dx value would represent the sampling period.

The C# code used to convert the doubles arrays to MIME strings is shown below. Converting back should be an straightforward exercise.

`

public override string ToJsonString()  
{  
string l = Convert.ToBase64String(GetBytes(Left));  
string r = Convert.ToBase64String(GetBytes(Right));  
return string.Format("{{ "SessionId":"{0}", "Dx":"{1}" "Left":"{2}", "Right":"{3}" }}", SessionId, Dx, l, r);  
};  

byte[] GetBytes(double[] vals);  
{  
var result = new byte[vals.Length * sizeof(double)];  
Buffer.BlockCopy(vals, 0, result, 0, result.Length);  
return result;  
};  

`

* * *

# REST API

* * *

## GET /Status/Version

Initializes the settings used in future acquisitions to the default state.

### Arguments

None.

### Example

`HTTP GET /Status/Version`  

* * *

## GET /Status/Connection

Indicates the status of the USB connection with the hardware. 'True' means connected.

### Arguments

None.

### Example

`HTTP GET /Status/Connection`  

* * *

## PUT /Settings/Default

Initializes the settings used in future acquisitions to the default state.

### Arguments

None.

### Example

`HTTP PUT /Settings/Default`  

* * *

## PUT /Settings/SampleRate/{SampleRate}

Sets the sample rate for the next acquisition.  

### Arguments

**SampleRate:** The sample rate in Hz. This must be either 48000 or 192000

### Example

`HTTP PUT /Settings/SampleRate/192000  

* * *

## PUT /Settings/RoundFrequencies/{Enable}

Automatically rounds generator frequencies to the near mid-bin value. This helps ensure spectral leakage is minimized. By default, this is enabled.

### Arguments

**Enable** 1=enabled, 0=disabled  

### Example

`HTTP PUT /Settings/RoundFrequencies/0  

The above code will disable the round frequencies behavior.  

* * *

## PUT /Settings/AudioGen/{Generator}/{On}/{Frequency}/{Amplitude}

Set the specified generator (1 or 2) to on or off (1=on, 0=off) to the specified frequency and amplitude. For example to set Gen1 on and at a level of 0 dBV and 1 KHz, you would issue  

`HTTP PUT localhost:9401/Settings/AudioGen/1/1/1000/0`  

### Arguments

**Generator** Specifies which audio generator is being assigned. Valid values are 1 or 2  
**On** Specifies if the generator should be 'on' (on = '1') or off (on = '0')  
**Frequency** Specifies the generator frequency, in Hz. Valid values are >= 1 Hz and <= 96000 Hz.  
**Amplitude** Specifies the generator amplitude in dBV. Valid values are >= -120 dBV and <= 6 dBV  

* * *

## PUT /Settings/BufferSize/{Size}

Sets the size of the buffer for the next acquisition.  

### Arguments

**Size:** The size of the acquisition buffer. This must be between 2048 and 262144 (inclusive) and must be a power of 2

### Example

`HTTP PUT /Settings/BufferSize/32768  

* * *

## PUT /Settings/Input/Max/{MaxInputLevelDbv}

Sets the attenuator state so that the maximum input level is the specified value.On the QA401, the allowed values are '6' and '26'. When '6' is specified, the maximum input value before clipping occurswill be +6 dBV. When '26' is specified, the maximum input value before clipping occurs is +26 dBV

### Arguments

**MaxInputLevelDbv:** The maximum allowed value before clipping will occur. Valid values are 6 dBV and 26 dBV  

### Example

`HTTP PUT /Settings/Input/Max/26  

* * *

## GET /ThdDb/{FundFreq}/{MaxFreq}

Gets the THD of the prior acquisition, expressed in decibels.  

### Arguments:

**FundFreq:** The frequency of the fundamental  
**MaxFreq:** The maximum frequency at which harmonics will be considered. This must be below the nyquist frequency (0.5 sample rate)  

### Example

`GET ThdDb/1000/20000`  

### Sample returned by server

{"SessionId":"286930", "Left":"-101.929476869617", "Right":"-98.8973249362777"}  

* * *

## GET /ThdPct/{FundFreq}/{MaxFreq}

Gets the THD of the prior acquisition, expressed in percent (0 to 100).

### Arguments:

**FundFreq:** The frequency of the fundamental  
**MaxFreq:** The maximum frequency at which harmonics will be considered. This should be below the nyquist frequency (0.5 sample rate)  

### Example:

`GET ThdPct/1000/20000`  

### Sample returned by server

{"SessionId":"286930", "Left":"0.001698239", "Right":"0.00153382"}  

* * *

## GET /ThdnDb/{FundFreq}/{MinFreq}/{MaxFreq}

Gets the THD+N of the prior acquisition, expressed in decibels.  

### Arguments:

**FundFreq:** The frequency of the fundamental  
**MinFreq:** The minimum used for the start of the noise calculation  
**MaxFreq:** The maximum frequency for the noise calculation. This should be below the nyquist frequency (0.5 sample rate)  

### Example

`GET ThdDb/1000/20000`  

### Sample returned by server

{"SessionId":"286930", "Left":"-101.929476869617", "Right":"-98.8973249362777"}  

* * *

## GET /ThdnPct/{FundFreq}/{MinFreq}/{MaxFreq}

Gets the THD of the prior acquisition, expressed in percent (0 to 100).

### Arguments:

**FundFreq:** The frequency of the fundamental  
**MinFreq:** The minimum used for the start of the noise calculation  
**MaxFreq:** The maximum frequency for the noise calculation. This should be below the nyquist frequency (0.5 sample rate)  

### Example:

`GET ThdPct/1000/20000`  

### Sample returned by server

{"SessionId":"286930", "Left":"0.001698239", "Right":"0.00153382"}  

* * *

## GET /RmsDbv/{StartFreq}/{EndFreq}

Computes the RMS of the prior acquisition, measured across the frequency bounds, and expressed in dBV

### Arguments:

**StartFreq:** The starting frequency for the computation.  
**EndFreq:** The ending frequency for the computation.  

### Example:

`GET RmsDbv/20/20000`

The code above will compute the RMS value in dBV of the acquired data from 20 to 20 KHz.

### Sample returned by server

{"SessionId":"286930", "Left":"-10.00", "Right":"-10.00"}  

* * *

## GET /RmsDbv/AWeighting/{StartFreq}/{EndFreq}

Computes the RMS of the prior acquisition, measured across the frequency bounds, and expressed in dBVwith AWeighting applied.

### Arguments:

**StartFreq:** The starting frequency for the computation.  
**EndFreq:** The ending frequency for the computation.  

### Example:

`GET RmsDbv/AWeighting/20/20000`  

### Sample returned by server

{"SessionId":"286930", "Left":"-10.00", "Right":"-10.00"}  

* * *

## GET /Phase/Degrees

Computes the phase difference in degrees between the output (reference) and input at the frequency specified by Generator 1\. In computing the phase, the QA401H first computes the absolute delay, in seconds, between the output and input by observing interpolated zero crossings averaged over several cycles. That delay is then converted to phase at the specified frequency of Generator 1.

### Arguments:

The request accepts no arguments.

### Example:

`GET Phase/Degrees`

### Sample returned by server

`{"SessionId":"286930", "Left":"-0.30", "Right":"-0.45"}`

* * *

## GET /Phase/Seconds

Computes the time difference in seconds between the output (reference) and input. In computing the phase, the QA401H computes the absolute delay, in seconds, between the output and input by observing interpolated zero crossings averaged over several cycles.

### Arguments:

The request accepts no arguments.

### Example:

`GET Phase/Seconds`  

### Sample returned by server

`{"SessionId":"286930", "Left":"-13.4e-6", "Right":"-13.4e-6"}`

The -13.4e-6 indicates the input lags the output by 13.4 uS  

* * *

## GET /Data/Freq/{Freq}

Returns the frequency data of the prior acquisition. The data will be returned in aJSON element, consisting of:SessionId:  

* * *

## GET /Graph/Frequency/In/{Channel}

Returns a PNG of the specified input channel data. The graph Y axis is log, with 10 dB/division spacing. The graph X axis is linear, ranging from 0 to 20 KHz. This is primarily to be used for developers doing sanity checks on measurements.

### Arguments:

**Channel:** Indicates left (= 0) or right (= 1) channel

### Example:

[`GET Graph/Frequency/In/0`](http://localhost:9401/Graph/Frequency/In/0)  

* * *

## GET /Graph/Frequency/AWeighting/In/{Channel}

Returns a PNG of the specified input channel data. The graph Y axis is log, with 10 dB/division spacing. The graph X axis is linear, ranging from 0 to 20 KHz. This is primarily to be used for developers doing sanity checks on measurements.

### Arguments:

**Channel:** Indicates left (= 0) or right (= 1) channel

### Example:

[`GET Graph/Frequency/In/0`](http://localhost:9401/Graph/Frequency/In/AWeighting/0)  

* * *

## POST /Acquisition

Starts a new acquisition [jump to top](http://localhost:9401/#TOP)  

* * *

`````
