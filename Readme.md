##Usage

    export OIDC=<OIDC Access Toeken>
    ./mccli https://cdmi-qos.data.kit.edu
    ./mccli http://diskserv-san-77.cr.cnaf.infn.it:9000
    ./mccli http://rhus-46.man.poznan.pl:80
    ./mccli https://cdmi-indigo.recas.ba.infn.it:8080
    ./mccli https://dcache-qos-01.desy.de:8443

The environment variable OIDC should contain a valid OIDC access token.
You can get one via https://tts.data.kit.edu => show me my token
functionality.

Proper output should look like this:

    Current Object:
    ---------------
    https://cdmi-qos.data.kit.edu/
                   capabilitiesURI :	  /cdmi_capabilities/container/CosSmallFilesE2EDP
                  completionStatus :	  Complete
                        objectType :	  application/cdmi-container
                     childrenrange :	  0-1
                          children : 
                                        test.txt
                                        test
                           exports : 
                                       "Network/WebDAV": 
                                       "identifier": "/hpss",
                                       "permissions": "domain"
                                   

    CDMI capabiliby class of this object:
    -------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/container/CosSmallFilesE2EDP
                cdmi_data_redundancy :	3
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	0
                     cdmi_throughput :	4194304

    =======================================================================================================================

    [marcus@tuna:~/grid/INDIGO/git/github/mccli]$ ./mccli -d https://cdmi-qos.data.kit.edu/test.txt
    Current Object:
    ---------------
    https://cdmi-qos.data.kit.edu/test.txt
                   capabilitiesURI :	  /cdmi_capabilities/dataobject/DiskAndTape
                  completionStatus :	  Complete
                        objectType :	  application/cdmi-object
                          mimetype :	  application/octet-stream

    CDMI capabiliby class of this object:
    -------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/dataobject/DiskAndTape
                cdmi_data_redundancy :	3
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	0
           cdmi_capabilities_allowed :	['/cdmi_capabilities/dataobject/TapeOnly', '/cdmi_capabilities/dataobject/DiskOnly']
                     cdmi_throughput :	4194304

    =======================================================================================================================
    Possible target CDMI capabiliby classes:
    ----------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/dataobject/TapeOnly
                cdmi_data_redundancy :	2
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	50000
           cdmi_capabilities_allowed :	['/cdmi_capabilities/dataobject/DiskAndTape']
                     cdmi_throughput :	4194304

        To move your object into this class, type:
        ./mccli https://cdmi-qos.data.kit.edu/test.txt --target /cdmi_capabilities/dataobject/TapeOnly
    ----------------------------------------
    https://cdmi-qos.data.kit.edu/cdmi_capabilities/dataobject/DiskOnly
                cdmi_data_redundancy :	1
           cdmi_geographic_placement :	['DE']
                        cdmi_latency :	0
           cdmi_capabilities_allowed :	['/cdmi_capabilities/dataobject/DiskAndTape']
                     cdmi_throughput :	4194304

        To move your object into this class, type:
        ./mccli https://cdmi-qos.data.kit.edu/test.txt --target /cdmi_capabilities/dataobject/DiskOnly
    =======================================================================================================================


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
