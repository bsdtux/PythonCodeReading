# Maya Reading
this file contains the reading of the maya library written by Kenneth Reitz
Maya was built to try and take the frustration out of working with datetimes in python

For basic usage see [maya](https://github.com/kennethreitz/maya)

# Dependencies for Maya 
humanize
pytz
dateparser
"ruamel.yaml"
tzlocal
pendulum
snaptime

# How the maya.now() method works
- Everything is imported from the maya package core module
- Declaration starts on line 668 of core module
- Creates an epoch time from the time library
- then returns an instance of the MayaDT class with the epoch time set to the above
- MayaDT inherits from object to create backwards compatability with python2
- Calls the parent class of super
- Sets the instance variable of epoch to the epoch parameter

# Intent
- After much conversation we came to the conclusion that Kenneth Reitz intends for the user of his library
to call one of the class methods and never instantiate the MayaDT class directly. 

- No matter what class method you call it is always reduced to using the epoch time.
- For example
    ```python
        @classmethod
    @validate_arguments_type_of_function(Datetime)
    def from_datetime(klass, dt):
        """Returns MayaDT instance from datetime."""
        return klass(klass.__dt_to_epoch(dt))
    ```

this will return an instance of MayaDT with the epoch time of the datetime object you passed in.

