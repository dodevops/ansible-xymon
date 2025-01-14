# ansible-xymon

    > XYMON    (/home/bert/.ansible/plugins/modules/xymon.py)
    
            A module to control states of hosts and test in Xymon.
    
    OPTIONS (= is mandatory):
    
    = host
            The host as specified in Xymon.

    - interval
            Required when specifying a colour as state (green, yellow, red) or disabled.
            It is the time in minutes the status stays valid in xymon. You can specify a unit by adding any of these four letter directly after the number: s, m, h, d.
            These are respectively for seconds, minutes, hours and days.
            Note: for disable Xs doesn't seem to work.
            There is one special value: -1 for when setting state disabled, which indicates disable until the first green monitoring event cames along.
            [Default: '30m']
    
    - msg
            Xymon message
            [Default: %timestamp% Set %state% by Ansible module xymon.]
    
    = state
            The desired state.
     
    - tests
            A comma separated list of tests as specified in Xymon.
            It is required for setting a color as state (green, yellow, red) and absent.
            Note that for absent by default, dropping a test in Xymon can only be done from the xymon host itself,
            so you'll need to specify something like delegate_to: xymonhost.
            If not specified (allowed with state disabled or enabled) it will effect all the tests on the host.
            [Default: '*']
    
    = xymon_host
            The hostname or IP address of the Xymon server.

    - xymon_port
            The port on which the Xymon server is listening.
            [Default: 1984]
    
    
    AUTHOR: Bert Raeymaekers (https://github.com/BertRaeymaekers)
    
    EXAMPLES:
    # Disable monitoring for one minute on all test of www.example.com:
    - xymon:
        xymon_host: 192.168.0.24
        host: www.example.com
        state: disabled
        interval: 1m
    
    # Disable monitoring for 5 minutes on test httpstatus on www.example.com:
    - xymon:
        xymon_host: 192.168.0.24
        host: www.example.com
        test: httpstatus
        state: disabled
        interval: 5

    # Disable monitoring for 5 minutes on tests httpstatus and cpu on www.example.com:
    - xymon:
        xymon_host: 192.168.0.24
        host: www.example.com
        tests: httpstatus,cpu
        state: disabled
        interval: 5

    # Enable monitoring for www.example.com:
    - xymon:
        xymon_host: 192.168.0.24
        host: www.example.com
        state: enabled
    
    RETURN VALUES:
~~~~
