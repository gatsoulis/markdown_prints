### QTC
QTC descirbes the movement of 2 agents in 2d space. The implemented version is described in [1,2].
Both agents need to have their x,y coordinates described for at least two timesteps. Please see `qsr_lib/share/qtc_data` or the `example_ros_client.py` for a very short example.

To run the ros example client uisng qtc:
```
rosrun qsr_lib example_ros_client.py <qtc-varaient>
```
This has a few options

* Mendatory: 
 * `<qtc-varaient>`: Can be either `qtcb`, `qtcc`, or `qtcbc`. Please refer to [1,2] for additional infromation about the variants
* Optional:
 * `-h|--help`: to display usage information
 * `-i|--input FILE`: read x,y coordinates from a csv file. See `qsr_lib/share/qtc_data/qtc_example.csv`
 * `--quantisation_factor FLOAT`: Determines the minimum distance one of the agents have to diverge from the double cross to be counted as movement. Please refer to [1] to read more about smoothing and quantisation of QTC.
 * `--validate`: Creates a QTC representation that is valid according to the CND [3]
 * `--no_collapse`: Does not collapse similar adjacent states as it the default in QTC since it does not represent discrete time but a sequence of states
 * `--distance_threshold`: Sets a threshold distance for the transition from QTCB to QTCC and vice-versa. Only for QTCBC [2].

To create a valid QTCC state chain with a quantisation factor of 1 (in the same unit as x,y) one would run:
```
  rosrun qsr_lib example_ros_client.py qtcc --validate --quantisation_factor 1 -i my_file.csv
```
To create a QTCB state for each transition from one timestep to the other without validating them, one would run:
```
  rosrun qsr_lib example_ros_client.py qtcb -i my_file.csv --no_collapse
```
To create a QTCBC state chain, one would run:
```
  rosrun qsr_lib example_ros_client.py qtcbc -i my_file.csv --distance_threshold 1.5 --validate
```

[1] Christian Dondrup, Nicola Bellotto, and Marc Hanheide. "A probabilistic model of human-robot spatial interaction using a qualitative trajectory calculus." 2014 AAAI Spring Symposium Series. 2014.

[2] Christian Dondrup, Nicola Bellotto, and Marc Hanheide. "Social distance augmented qualitative trajectory calculus for Human-Robot Spatial Interaction." Robot and Human Interactive Communication, 2014 RO-MAN: The 23rd IEEE International Symposium on. IEEE, 2014.

[3] Matthias Delafontaine. "Modelling and analysing moving objects and travelling subjects: Bridging theory and practice". Diss. Ghent University, 2011.
