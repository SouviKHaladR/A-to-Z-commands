
								Ansible all commands

Ad-hoc commands

Ping localhost: # ansible localhost –m ping

Creating a file on all remote clients: # ansible all –m file –a “path=/home/ansible/adhoc1 state=touch mode=700”

Deleting a file on all remote clients: # ansible all –m file –a “path=/home/ansible/adhoc1 state=absent”

Copying a file to remote clients: # ansible all –m copy –a “src=/tmp/adhoc2 dest=/home/ansible/adhoc2”

Installing package (telnet and httpd-manual): # ansible all –m yum –a “name=telnet state=present” # ansible all –m yum –a “name=httpd-manual state=present”

Starting httpd package service: # ansible all –m service –a “name=httpd state=started”

Start httpd and enable at boot time: # ansible all –m service –a “name=httpd state=started enabled=yes”

Checking httpd service status on remote client: # ansible all –m shell -a “systemctl status httpd”

Remove httpd package: # ansible all –m yum –a “name=httpd state=absent” OR # ansible all –m shell -a “yum remove httpd”.

Creating a user on remote clients: # ansible all –m user –a “name=ansible home=/home/ansible shell=/bin/bash state=present”

To add a user to a different group: # ansible all –m user –a “name=ansible group=ansible”

Deleting a user on remote clients: # ansible all –m user –a “name=ansible home=/home/ansible shell=/bin/bash state=absent”
OR
# ansible all –m shell –a “userdel ansible”

Getting system information from remote clients: # ansible all –m setup

You can run commands on the remote host without a shell module e.g. reboot client1: # ansible client1 –a “/sbin/reboot”


Ansible Playbook Commands:

ansible-playbook <playbook.yml>: This is the simplest form. It executes the playbook named <playbook.yml> from your current working directory.

ansible-playbook -i <inventory_file> <playbook.yml>: This allows you to specify a non-default inventory file to target specific hosts or groups.

ansible-playbook --syntax-check <playbook.yml>: Checks the playbook for syntax errors without actually running it.

ansible-playbook --diff <playbook.yml>: Performs a dry-run, showing changes that would be made if the playbook were executed without applying them.

ansible-playbook <playbook.yml> -l <hostname_or_group>: This targets a specific host or group from your inventory. You can use -G for all groups matching a pattern.

ansible-playbook -v <playbook.yml>: Increases verbosity level (use multiple -v flags for more details).

ansible-playbook -q <playbook.yml>: Runs the playbook quietly, with minimal output.

ansible-playbook --limit <hostname_or_group>: Similar to -l but restricts further execution even if errors occur on the targeted hosts/groups.

ansible-playbook --extra-vars <key=value>: Injects additional variables directly into the playbook for temporary use (can be repeated for multiple key-value pairs).

ansible-playbook --tags <tag_name>: Executes only tasks within the playbook that have the specified tag. You can use -t as a shorthand.

ansible-playbook --skip-tags <tag_name>: Skips tasks with the specified tag. You can use -s as a shorthand.


Ansible Pull Commands:

ansible-pull: This executes the ansible-pull command with default settings, assuming a playbook named local.yml exists in the configured location.

ansible-pull <playbook_name.yml>: This allows you to specify a different playbook name to execute.

ansible-pull -U <repository_url>: Defines the URL of the version control system (VCS) repository where your playbooks reside.

ansible-pull -C <branch_or_tag>: Specifies the branch or tag to pull content from within the repository.

ansible-pull -i <inventory_file>: Sets the location of the inventory file used by the playbook (defaults to the configured location for ansible-pull).

ansible-pull --diff: Performs a dry-run, showing changes that would be made if the playbook were executed without actually applying them.


Ansible Vault commands:

ansible-vault create <filename>: Creates a new encrypted file for storing secrets.

ansible-vault edit <filename>: Opens the encrypted file in your default editor for modification. You'll be prompted for the vault password.

ansible-vault view <filename>: Displays the decrypted content of the file without modifying it. Requires the vault password.

ansible-vault encrypt <filename>: Encrypts a plain text file.

ansible-vault decrypt <filename>: Decrypts an already encrypted file. (Use with caution, might expose sensitive data)

ansible-vault encrypt_string <string>: Encrypts a string value for immediate use in playbooks.

ansible-vault rekey <filename>: Changes the encryption key for an existing vault file. Useful for rotating passwords.

ansible-vault prompts for the password.

ansible-vault --ask-vault-pass: Prompts for the password every time.

ansible-vault --vault-password-file <file>: Reads password from a specified file.


Ansible Test Commands:

ansible-test sanity: Runs basic sanity checks like linting and static code analysis.

ansible-test units: Executes unit tests for modules and plugins.

ansible-test integration: Runs integration tests for playbooks and their interactions with external systems.

ansible-test --coverage: Generates test coverage reports. You can use further options like html, xml to specify report formats.

ansible-test --verbose: Enables verbose output for the tests, providing more details about execution and results.

ansible-test --help: Displays general help information about the ansible-test command and its options.

ansible-test shell: Opens an interactive shell within the same environment used to run tests. This can be useful for debugging purposes. You can use options like --docker or --venv to specify a Docker container or Python virtual environment for the shell.


Ansible Config Commands:

ansible-config: Displays all configured options and their current values from the various configuration files Ansible reads.

ansible-config <option_name>: Shows the value of a specific configuration option.

ansible-config --list: Lists all available configuration options Ansible recognizes, along with their descriptions (if defined).

ansible-config -v: Enables verbose mode, providing additional details about the configuration and search paths. You can use multiple -v flags (e.g., -vvv) for increasing verbosity levels.

ansible-config --version: Displays the version of ansible-config and related details like Ansible's configuration file location and module paths.

ansible-config --help: Provides general help information about the ansible-config command and its options.


Ansible Doc Commands:

ansible-doc <module_name>: This is the simplest form. It retrieves and displays documentation for a specific Ansible module.

ansible-doc [-t <plugin_type>]: Use the -t option with a plugin type (e.g., command, module) to filter the output for that specific type. By default, it focuses on modules.

ansible-doc <collection_name>/<module_name>: For modules within Ansible collections (introduced in Ansible 2.9), specify the collection name followed by a forward slash and then the module name.

ansible-doc [-M <module_path>]: This lets you specify additional module search paths if your modules reside outside the default locations. Separate multiple paths with colons.

ansible-doc [-l | --list]: Lists all available modules, plugins, and their types without summaries.

ansible-doc [-j | --json]: Outputs the documentation information in JSON format, useful for scripting or integration with other tools.

ansible-doc [-r <roles_path>]: If you're working with roles, this option specifies the path to search for role documentation.

ansible-doc --version: Displays the version of ansible-doc you're using.

ansible-doc --help: Provides general help information about the ansible-doc command and its options.


Ansible Galaxy commands 

ansible-galaxy install <role_name>: Downloads and installs a role from Ansible Galaxy.

ansible-galaxy list: Lists all installed roles with their versions.

ansible-galaxy info <role_name>: Shows detailed information about a specific installed role.

ansible-galaxy remove <role_name>: Removes an installed role.

ansible-galaxy init <role_name>: Initializes a new role template directory structure.

ansible-galaxy collection install <collection_name>: Downloads and installs a collection from Ansible Galaxy.

ansible-galaxy collection list: Lists all installed collections with their versions.

ansible-galaxy collection verify <collection_name>: Verifies the integrity of an installed collection.

ansible-galaxy login: Authenticates with Ansible Galaxy to perform actions like publishing roles (requires an account).

ansible-galaxy search <search_term>: Searches for roles or collections in Ansible Galaxy.


Ansible Inventory Commands:

ansible-inventory --list: This is the most common usage. It displays the entire inventory structure, including groups and hosts, in JSON format by default.

ansible-inventory --host <hostname>: Shows detailed information about a particular host from your inventory.

ansible-inventory --list [group_name]: Lists only the specified group and its contents (subgroups and hosts).

ansible-inventory --list --export: Presents the inventory data in a format optimized for exporting, not necessarily reflecting the exact structure Ansible uses internally.

ansible-inventory --list --toml: Outputs the inventory information in TOML format instead of the default JSON.

ansible-inventory --graph [group_name] (optional): Generates an ASCII art visualization of the inventory, useful for understanding group hierarchies. If you provide a group name, the graph will be centered around that group.

ansible-inventory -i <inventory_file>: Specifies a non-default inventory file to manage. The default location is usually inventory.ini.

ansible-inventory --playbook-dir <directory>: While ansible-inventory doesn't directly work with playbooks, this option sets the relative path for features like group_vars and host_vars directories used by playbooks in the specified directory.

ansible-inventory --vars: Combines host and group variables with inventory data when using the --graph option.


Ansible Navigator commands:

ansible-navigator: Launches the Ansible Navigator TUI in interactive mode.

ansible-navigator --help: Displays general help information about Ansible Navigator.

ansible-navigator config: Shows and explores your Ansible configuration settings.

ansible-navigator doc <module_name>: Retrieves and displays documentation for a specific Ansible module.

ansible-navigator collections: Lists and explores available Ansible collections.

ansible-navigator inventory: Examines and interacts with your Ansible inventory file.

ansible-navigator images: Lists execution environment Docker images available locally.

ansible-navigator run <playbook_name>: Executes a chosen playbook. You can specify the inventory file with -i <inventory_file>.

ansible-navigator replay: Analyzes results from a previous playbook run using a playbook artifact.

ansible-navigator settings: Manages Ansible Navigator settings.
