# scratchpad

_(development notes etc)_


## NMEA sample

	$GPRMC,210209.000,V,5347.5779,N,00754.1630,E,000.0,000.0,300717,,,N*77
	$GPGGA,210210.000,5347.5779,N,00754.1630,E,0,00,0.0,52.8,M,0.0,M,,0000*59

## NMEA data structure

based on information by [Dale DePriest]( http://www.gpsinformation.org/dale/nmea.htm )

### GGA - essential fix data which provide 3D location and accuracy data.

	$GPGGA,123519,4807.038,N,01131.000,E,1,08,0.9,545.4,M,46.9,M,,*47

- GGA : Global Positioning System Fix Data
- 123519 : Fix taken at 12:35:19 UTC
- 4807.038,N : Latitude 48 deg 07.038' N
- 01131.000,E : Longitude 11 deg 31.000' E
- 1 : Fix quality: 0 = invalid, 1 = GPS fix (SPS), 2 = DGPS fix, 3 = PPS fix, 4 = Real Time Kinematic, 5 = Float RTK, 6 = estimated (dead reckoning) (2.3 feature), 7 = Manual input mode, 8 = Simulation mode
- 08 : Number of satellites being tracked
- 0.9 : Horizontal dilution of position
- 545.4,M : Altitude, Meters, above mean sea level
- 46.9,M : Height of geoid (mean sea level) above WGS84 ellipsoid
- (empty field) : time in seconds since last DGPS update
- (empty field) : DGPS station ID number
- *47 : checksum data, always begins with *

_If the height of geoid is missing then the altitude should be suspect. Some non-standard implementations report altitude with respect to the ellipsoid rather than geoid altitude. Some units do not report negative altitudes at all. This is the only sentence that reports altitude._

### RMC - essential gps pvt (position, velocity, time) data

	$GPRMC,123519,A,4807.038,N,01131.000,E,022.4,084.4,230394,003.1,W*6A

- RMC : Recommended Minimum sentence C
- 123519 : Fix taken at 12:35:19 UTC
- A : Status A=active or V=Void.
- 4807.038,N : Latitude 48 deg 07.038' N
- 01131.000,E Longitude 11 deg 31.000' E
- 022.4 : Speed over the ground in knots
- 084.4 : Track angle in degrees True
- 230394 : Date - 23rd of March 1994
- 003.1,W : Magnetic Variation
- *6A : The checksum data, always begins with *
