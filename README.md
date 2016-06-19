# libfilter
An Arduino-compatible C++ library for simple signal filtering. 

As of this writing, the library implements low-pass filters up to the fourth order. 
Filters are based on [normalized Butterworth polynomials](https://en.wikipedia.org/wiki/Butterworth_filter).

## Using it 

### With Arduino

Copy the `libFilter` folder into your `libraries` folder. The following example sketch is included:

    #include <filters.h>
    
    const float cutoff_freq   = 20.0;  //Cutoff frequency in Hz
    const float sampling_time = 0.005; //Sampling time in seconds.
    IIR::ORDER  order  = IIR::ORDER::OD3; // Order (OD1 to OD4)
    
    // Low-pass filter
    Filter f(cutoff_freq, sampling_time, order);
    
    void setup() {
      Serial.begin(115200);
      pinMode(A0, INPUT);
      // Enable pull-ups if necessary
      digitalWrite(A0, HIGH);
    }
    
    void loop() {
      int value = analogRead(0);
      float filteredval = f.filterIn(value);
      //View with Serial Plotter
      Serial.print(value, DEC);
      Serial.print(",");
      Serial.println(filteredval, 4);
      delay(5); // Loop time will approx. match the sampling time.
    }
