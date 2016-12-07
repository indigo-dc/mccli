##Usage

export OIDC=<OIDC Access Toeken>
./mccli https://cdmi-qos.data.kit.edu

The environment variable OIDC should contain a valid OIDC access token.
You can get one via https://tts.data.kit.edu => show me my token
functionality.

Proper output should look like this:

    ./mccli --oidc $OIDC https://cdmi-qos.data.kit.edu/test.txt
    Current Object:
    ---------------
    https://cdmi-qos.data.kit.edu/test.txt
                   capabilitiesURI :	  /cdmi_capabilities/dataobject/TapeOnly
                  completionStatus :	  Complete
                        objectType :	  application/cdmi-object
                          mimetype :	  application/octet-stream
    
    CDMI capabiliby class of this object:
    -------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/dataobject/TapeOnly
    my_caps: ['cdmi_data_redundancy', 'cdmi_geographic_placement', 'cdmi_latency', 'cdmi_capabilities_allowed', 'cdmi_throughput']
                cdmi_data_redundancy :	2
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	50000
           cdmi_capabilities_allowed :	['/cdmi_capabilities/dataobject/DiskAndTape']
                     cdmi_throughput :	4194304
    
    Possible target CDMI capabiliby classes:
    ----------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/dataobject/DiskAndTape
    my_caps: ['cdmi_data_redundancy', 'cdmi_geographic_placement', 'cdmi_latency', 'cdmi_capabilities_allowed', 'cdmi_throughput']
                cdmi_data_redundancy :	3
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	0
           cdmi_capabilities_allowed :	['/cdmi_capabilities/dataobject/TapeOnly', '/cdmi_capabilities/dataobject/DiskOnly']
                     cdmi_throughput :	4194304
    
    To move your object into this class, type:
    ./mccli https://cdmi-qos.data.kit.edu/test.txt --target /cdmi_capabilities/dataobject/DiskAndTape


##Parameters:
 
    usage: mccli [-h] [--verbose] [--raw] [--all-classes] [--dest-classes]
                 [--user CDMI_USER] [--pass CDMI_PASS] [--oidc CDMI_OIDC]
                 [--target CDMI_TARGET_CAPABILITY_CLASS] [--short]
                 [--cachedir CACHEDIR]
                 URL

    Marcus Cdmi CLI

    positional arguments:
      URL                   URL of file on CMDI server (for example: https://cdmi-
                            qos.data.kit.edu/test.txt

    optional arguments:
      -h, --help            show this help message and exit
      --verbose, -v         Show more debug output. Can be used multiple times
      --raw, -r             Show raw json output. Can be used multiple times. Use
                            twice to show json and intepreted output
      --all-classes, -a     Show all available storage classes of given CDMI
                            server
      --dest-classes, -d    Show possible destination classes for given CDMI
                            object
      --user CDMI_USER      Username
      --pass CDMI_PASS      Password
      --oidc CDMI_OIDC, -o CDMI_OIDC
                            OpenID-Connect token (exported environment variables
                            will be used as a default: export OIDC=<token>
      --target CDMI_TARGET_CAPABILITY_CLASS
                            Target cdmi capability class to stage object to
      --short, -s           Be concise
      --cachedir CACHEDIR, -c CACHEDIR
                            Dir to cache cdmi responses. Useful for offline
                            testing. Default: /tmp/mccli
