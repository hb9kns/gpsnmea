# scratchpad

_(development notes etc)_


## NMEA sample

	$GPGGA,210210.000,5347.5779,N,00754.1630,E,0,00,0.0,52.8,M,0.0,M,,0000*59
	$GPRMC,210209.000,V,5347.5779,N,00754.1630,E,000.0,000.0,300717,,,N*77

## NMEA data structure

based on information by [Dale DePriest]( http://www.gpsinformation.org/dale/nmea.htm )

### GGA - essential fix data which provide 3D location and accuracy data.

	$GPGGA,210210.000,5347.5779,N,00754.1630,E,0,00,0.0,52.8,M,0.0,M,,0000*59

- GGA : Global Positioning System Fix Data
- 210210.000 : Fix taken at 21:02:10 UTC (.NNN seems to vary randomly)
- 5347.5779,N : Latitude 53 deg 47.5779 min N
- 00754.1630,E : Longitude 7 deg 54.1630 min E
- 0 : Fix quality: 0 = invalid, 1 = GPS fix (SPS), 2 = DGPS fix, 3 = PPS fix, 4 = Real Time Kinematic, 5 = Float RTK, 6 = estimated (dead reckoning) (2.3 feature), 7 = Manual input mode, 8 = Simulation mode
- 00 : Number of satellites being tracked
- 0.0 : Horizontal dilution of position
- 52.8,M : Altitude, Meters, above mean sea level
- 0.0,M : Height of geoid (mean sea level) above WGS84 ellipsoid
- (empty field) : time in seconds since last DGPS update
- 0000 : DGPS station ID number
- `*59` : checksum data, always begins with `*`

_If the height of geoid is missing then the altitude should be suspect. Some non-standard implementations report altitude with respect to the ellipsoid rather than geoid altitude. Some units do not report negative altitudes at all. This is the only sentence that reports altitude._

### RMC - essential gps pvt (position, velocity, time) data

	$GPRMC,210209.000,V,5347.5779,N,00754.1630,E,000.0,000.0,300717,,,N*77

- RMC : Recommended Minimum sentence C
- 210209.000 : Fix taken at 21:02:09 UTC (.NNN seems to vary randomly)
- V : Status A=active or V=Void.
- 5347.5779,N : Latitude 53 deg 47.5779 min N
- 00754.1630,E : Longitude 7 deg 54.1630 min E
- 000.0 : Speed over the ground in knots
- 000.0 : Track angle in degrees True
- 300717 : Date - 30th of July 2017
- (empty field) : _unknown_
- (empty field),N : Magnetic Variation (?)
- `*77` : checksum data, always begins with `*`
