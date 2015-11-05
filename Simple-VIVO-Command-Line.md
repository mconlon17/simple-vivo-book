# Simple VIVO Command Line

Here we describe the command line parameters and how each is used.

To see the available Simple VIVO command line paraemters and get a brief description of each one, go to
the command line and type

    python sv.py -h

You will see the display below.

    Get or update row and column data from and to VIVO
    
    optional arguments:
      -h, --help            show this help message and exit
      -a [ACTION], --action [ACTION]
                            desired action. get = get data from VIVO. update =
                            update VIVO data from a spreadsheet. summarize = show
                            def summary. serialize = serial version of the pump. test = test connection to VIVO.
      -d [DEFN], --defn [DEFN]
                            name of definition file
      -i [INTER], --inter [INTER]
                            interfield delimiter
      -j [INTRA], --intra [INTRA]
                            intrafield delimiter
      -u [USERNAME], --username [USERNAME]
                            username for API
      -p [PASSWORD], --password [PASSWORD]
                            password for API
      -q [QUERYURI], --queryuri [QUERYURI]
                            URI for API
      -r [RDFPREFIX], --rdfprefix [RDFPREFIX]
                            RDF prefix
      -x [URIPREFIX], --uriprefix [URIPREFIX]
                            URI prefix
      -s [SRC], --src [SRC]
                            name of source file containing data to be updated in
                            VIVO
      -c [CONFIG], --config [CONFIG]
                            name of file containing config data. Config data
                            overrides program defaults. Command line overrides
                            config file values
      -v, --verbose         write verbose processing messages to the log
      -n, --nofilters       turn off filters
    
    For more info, see http://github.com/mconlon17/vivo-pump
    
See [Getting Started](Getting-Started.md) for a description of `username`, `password`, `queryuri`, and `uriprefix`.
Each is specific to your site and must be correct for Simple VIVO to work.  We recommend putting these values in the
Simple VIVO config file so that they do not have to be put on the command line.