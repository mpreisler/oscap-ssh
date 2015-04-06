# oscap-ssh
## Usage
```
oscap-ssh user@host 22 xccdf eval INPUT_CONTENT

Only source datastreams are supported as INPUT_CONTENT!

supported oscap options are:
  --profile
  --results
  --results-arf
  --report
  --tailoring-file
```

## Example 1

The following command evaluates a remote Fedora machine as root. HTML report is written out as report.html on the local machine. Can be executed from any machine that has ssh, scp and bash. The local machine does not need openscap installed.

```
./oscap-ssh root@192.168.1.13 22 xccdf eval --profile xccdf_org.ssgproject.content_profile_common --report report.html /usr/share/xml/scap/ssg/content/ssg-fedora-ds.xml
```

The output:
```
Connecting to 'root@192.168.1.13' on port '22'...
root@192.168.1.13's password: 
Connected!
Copying input file '/usr/share/xml/scap/ssg/content/ssg-fedora-ds.xml' to remote working directory '/tmp/tmp.yEsdWV54ry'...
ssg-fedora-ds.xml                                                                                                                                                                                            100%  683KB 683.2KB/s   00:00    
Starting the evaluation...
Title   gpgcheck Enabled In Main Yum Configuration
Rule    xccdf_org.ssgproject.content_rule_ensure_gpgcheck_globally_activated
Result  pass

Title   gpgcheck Enabled For All Yum Package Repositories
Rule    xccdf_org.ssgproject.content_rule_ensure_gpgcheck_never_disabled
Result  fail

Title   Disable Prelinking
Rule    xccdf_org.ssgproject.content_rule_disable_prelink
Result  fail

Title   Shared Library Files Have Restrictive Permissions
Rule    xccdf_org.ssgproject.content_rule_file_permissions_library_dirs
Result  fail

Title   Shared Library Files Have Root Ownership
Rule    xccdf_org.ssgproject.content_rule_file_ownership_library_dirs
Result  pass

Title   System Executables Have Restrictive Permissions
Rule    xccdf_org.ssgproject.content_rule_file_permissions_binary_dirs
Result  pass

Title   System Executables Have Root Ownership
Rule    xccdf_org.ssgproject.content_rule_file_ownership_binary_dirs
Result  pass

Title   Direct root Logins Not Allowed
Rule    xccdf_org.ssgproject.content_rule_no_direct_root_logins
Result  notchecked

Title   Virtual Console Root Logins Restricted
Rule    xccdf_org.ssgproject.content_rule_securetty_root_login_console_only
Result  pass

Title   Serial Port Root Logins Restricted
Rule    xccdf_org.ssgproject.content_rule_restrict_serial_port_logins
Result  pass

Title   Only Root Has UID 0
Rule    xccdf_org.ssgproject.content_rule_no_uidzero_except_root
Result  pass

Title   Log In to Accounts With Empty Password Impossible
Rule    xccdf_org.ssgproject.content_rule_no_empty_passwords
Result  fail

Title   Password Hashes For Each Account Shadowed
Rule    xccdf_org.ssgproject.content_rule_no_hashes_outside_shadow
Result  pass

Title   netrc Files Do Not Exist
Rule    xccdf_org.ssgproject.content_rule_no_netrc_files
Result  pass

Title   Password Minimum Length
Rule    xccdf_org.ssgproject.content_rule_accounts_password_minlen_login_defs
Result  fail

Title   Password Minimum Age
Rule    xccdf_org.ssgproject.content_rule_accounts_minimum_age_login_defs
Result  fail

Title   Password Maximum Age
Rule    xccdf_org.ssgproject.content_rule_accounts_maximum_age_login_defs
Result  fail

Title   Password Warning Age
Rule    xccdf_org.ssgproject.content_rule_accounts_password_warn_age_login_defs
Result  pass

Title   Ensure that Root's Path Does Not Include World or Group-Writable Directories
Rule    xccdf_org.ssgproject.content_rule_root_path_no_groupother_writable
Result  pass

Title   SSH Root Login Disabled
Rule    xccdf_org.ssgproject.content_rule_sshd_disable_root_login
Result  pass

Title   SSH Access via Empty Passwords Disabled
Rule    xccdf_org.ssgproject.content_rule_sshd_disable_empty_passwords
Result  pass

Title   SSH Idle Timeout Interval Used
Rule    xccdf_org.ssgproject.content_rule_sshd_set_idle_timeout
Result  pass

Title   SSH Client Alive Count Used
Rule    xccdf_org.ssgproject.content_rule_sshd_set_keepalive
Result  pass

Title   Enable the NTP Daemon
Rule    xccdf_org.ssgproject.content_rule_service_ntpd_enabled
Result  fail

Title   Specify a Remote NTP Server
Rule    xccdf_org.ssgproject.content_rule_ntpd_specify_remote_server
Result  fail

oscap exit code: 2
Copying back requested files...
report.html                                                                                                                                                                                                  100%  619KB 619.0KB/s   00:00    
Removing remote temporary directory...
Disconnecting ssh and removing master ssh socket directory...
```

## Example 2

A more full example, uses a tailoring file and also copies back ARF, XCCDF results. The tailoring file is copied from local machine to remote.

```
./oscap-ssh root@192.168.1.13 22 xccdf eval --profile xccdf_org.ssgproject.content_profile_common --report report.html --results results.xml --results-arf arf.xml --tailoring-file ssg-fedora-ds-tailoring.xml /usr/share/xml/scap/ssg/content/ssg-fedora-ds.xml
```

The output:
```
Connecting to 'root@192.168.1.13' on port '22'...
root@192.168.1.13's password: 
Connected!
Copying input file '/usr/share/xml/scap/ssg/content/ssg-fedora-ds.xml' to remote working directory '/tmp/tmp.yVy6snyC88'...
ssg-fedora-ds.xml                                                                                                                                                                                            100%  683KB 683.2KB/s   00:00    
Copying tailoring file 'ssg-fedora-ds-tailoring.xml' to remote working directory '/tmp/tmp.yVy6snyC88'...
ssg-fedora-ds-tailoring.xml                                                                                                                                                                                  100% 1248     1.2KB/s   00:00    
Starting the evaluation...
Title   gpgcheck Enabled In Main Yum Configuration
Rule    xccdf_org.ssgproject.content_rule_ensure_gpgcheck_globally_activated
Result  pass

Title   gpgcheck Enabled For All Yum Package Repositories
Rule    xccdf_org.ssgproject.content_rule_ensure_gpgcheck_never_disabled
Result  fail

Title   Disable Prelinking
Rule    xccdf_org.ssgproject.content_rule_disable_prelink
Result  fail

Title   Shared Library Files Have Restrictive Permissions
Rule    xccdf_org.ssgproject.content_rule_file_permissions_library_dirs
Result  fail

Title   Shared Library Files Have Root Ownership
Rule    xccdf_org.ssgproject.content_rule_file_ownership_library_dirs
Result  pass

Title   System Executables Have Restrictive Permissions
Rule    xccdf_org.ssgproject.content_rule_file_permissions_binary_dirs
Result  pass

Title   System Executables Have Root Ownership
Rule    xccdf_org.ssgproject.content_rule_file_ownership_binary_dirs
Result  pass

Title   Direct root Logins Not Allowed
Rule    xccdf_org.ssgproject.content_rule_no_direct_root_logins
Result  notchecked

Title   Virtual Console Root Logins Restricted
Rule    xccdf_org.ssgproject.content_rule_securetty_root_login_console_only
Result  pass

Title   Serial Port Root Logins Restricted
Rule    xccdf_org.ssgproject.content_rule_restrict_serial_port_logins
Result  pass

Title   Only Root Has UID 0
Rule    xccdf_org.ssgproject.content_rule_no_uidzero_except_root
Result  pass

Title   Log In to Accounts With Empty Password Impossible
Rule    xccdf_org.ssgproject.content_rule_no_empty_passwords
Result  fail

Title   Password Hashes For Each Account Shadowed
Rule    xccdf_org.ssgproject.content_rule_no_hashes_outside_shadow
Result  pass

Title   netrc Files Do Not Exist
Rule    xccdf_org.ssgproject.content_rule_no_netrc_files
Result  pass

Title   Password Minimum Length
Rule    xccdf_org.ssgproject.content_rule_accounts_password_minlen_login_defs
Result  fail

Title   Password Minimum Age
Rule    xccdf_org.ssgproject.content_rule_accounts_minimum_age_login_defs
Result  fail

Title   Password Maximum Age
Rule    xccdf_org.ssgproject.content_rule_accounts_maximum_age_login_defs
Result  fail

Title   Password Warning Age
Rule    xccdf_org.ssgproject.content_rule_accounts_password_warn_age_login_defs
Result  pass

Title   Ensure that Root's Path Does Not Include World or Group-Writable Directories
Rule    xccdf_org.ssgproject.content_rule_root_path_no_groupother_writable
Result  pass

Title   SSH Root Login Disabled
Rule    xccdf_org.ssgproject.content_rule_sshd_disable_root_login
Result  pass

Title   SSH Access via Empty Passwords Disabled
Rule    xccdf_org.ssgproject.content_rule_sshd_disable_empty_passwords
Result  pass

Title   SSH Idle Timeout Interval Used
Rule    xccdf_org.ssgproject.content_rule_sshd_set_idle_timeout
Result  pass

Title   SSH Client Alive Count Used
Rule    xccdf_org.ssgproject.content_rule_sshd_set_keepalive
Result  pass

Title   Enable the NTP Daemon
Rule    xccdf_org.ssgproject.content_rule_service_ntpd_enabled
Result  fail

Title   Specify a Remote NTP Server
Rule    xccdf_org.ssgproject.content_rule_ntpd_specify_remote_server
Result  fail

oscap exit code: 2
Copying back requested files...
results-xccdf.xml                                                                                                                                                                                            100%  475KB 474.8KB/s   00:00    
results-arf.xml                                                                                                                                                                                              100% 1164KB   1.1MB/s   00:00    
report.html                                                                                                                                                                                                  100%  619KB 619.0KB/s   00:00    
Removing remote temporary directory...
Disconnecting ssh and removing master ssh socket directory...
```
