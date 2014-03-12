## FreeBSD make buildworld Ansible role

This role tries to automate a make buildworld. Since a make buildworld can take several hours to execute and needs to match the FreeBSD version, the role provides a few safeguards to avoid executing a buildworld when some conditions are not met.

1. A boolean buildworld_activated can be used to switch off the role
2. Only extracts a src.txz if /usr/src/README exists
3. Will fail if it cannot grep buildworld_src_readme_grep_line in the README (see defaults/main.yml)

The role providesa strategy involving a state file which existance indicates that the build has completed. The build will not be run unless the state file does not exists. This strategy provides idempotency, and is useful since make buildworld typically takes a few hours and will fail if the ssh connection disconnects. (see defaults/main.yml for the variables that control the state file)
