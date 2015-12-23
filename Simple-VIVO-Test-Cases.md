# Simple VIVO Test Cases

Simple VIVO can be tested using `test_sv.py` in the `tests` directory.  Various tests are performed and test results
reported along with timings of each test.

## Running the Tests

To run the tests, open a terminal window, navigate to the `tests` directory and use:

    python test_sv.py
    
Test results will be displayed in your terminal window.  Sample test output is shown below.  Three items are displayed
for each test:

1. The name of the test.  `config not found` is the name of a test that demonstrates Simple VIVO behaviour when 
the configuration file is not found.
1.  The return code.  Simple VIVO returns `0` if no errors occured.  Simple VIVO returns `1` if errors occurred.
For the `config not found` test, the configuration file was not found.  This is an error.  Simple VIVO produces
a return code of `1`.
1. The time in seconds to complete the test.  Timings were done with a Simple VIVO and a VIVO Vagrant running 
on a MacBook.


              config not found 	1 	0.112974
     definition file not found 	1 	0.044921
                          help 	0 	0.052848
         source file not found 	1 	0.114163
                          test 	0 	0.880568

