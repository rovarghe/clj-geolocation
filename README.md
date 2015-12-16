# clj-geolocation

Clojure functions to find geodesic between points (on Earth) and bounding co-ordinates within a radius of given location.

## Acknowledgement

Original paper at http://janmatuschek.de/LatitudeLongitudeBoundingCoordinates

## Usage

```
(require '[geolocation.core :as g])

;; Create geo-locations
(def LAX (g/from-degrees 33.9415933,-118.410724))
(def SFO (g/from-degrees 37.6213171,-122.3811494))
(def JFK (g/from-radians 0.7093247608354885,-1.2877097358131546))

;; Distance between two locations on Earth, in kilometers
(g/distance LAX SFO)
>> 543.6600860695804

(g/distance SFO JFK)
>>4152.0531696692005

(g/distance LAX JFK)
>>3974.335626005353

(def RADIUS-OF-JUPITER (* 200 g/EARTH-RADIUS))

;; Optional third argument - radius of sphere
(g/distance LAX SFO RADIUS-OF-JUPITER)
>>108732.0172...

```

Bounds of square around JFK inscribing a circle (lying on a sphere) with radius of 10 kms.

*On Earth:*

```
;; Returns 2 pairs of [lat lon] values representing corners of the square
(mapv g/to-degrees (g/bounds JFK 10))
>>[[40.55138293940813 -73.89885177280358] [40.73124726059187 -73.6618144271964]]
```

*On Jupiter:*

```
;; Change radius of circle
(mapv g/to-degrees (g/bounds JFK 10 RADIUS-OF-JUPITER))
>>[[40.64086543919704 -73.78092569318474] [40.64176476080296 -73.77974050681524]]
```

## License

Distributed under the Creative Commons Attributions License.

http://creativecommons.org/licenses/by/3.0
