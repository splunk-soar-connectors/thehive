## Playbook Backward Compatibility

- The below-mentioned action has been added. Hence, it is requested to the end-user to please
  update their existing playbooks by inserting the corresponding action blocks for this action on
  the earlier versions of the app.

  - create task log

- The existing output data paths have been modified for the 'get observables' action. Hence, it is
  requested to the end-user to please update their existing playbooks by re-inserting | modifying
  | deleting the corresponding action blocks to ensure the correct functioning of the playbooks
  created on the earlier versions of the app.

Note: The asset configuration parameter 'timezone', will be used for the 'occur_date' parameter in
the 'add ttp' action.

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the TheHive server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http | tcp | 80 |
|         https | tcp | 443 |
