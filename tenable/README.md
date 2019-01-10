Nessus Agent Ansible Role
=========================

## Purpose

Helps automating the deployment and configuration of the [Nessus Agent](https://www.tenable.com/products/nessus/nessus-agents).

## Supported Platforms

See [meta info](meta/main.yml).

## User Manual

### Basic usage

* Add the role to your project's Ansible galaxy requirements file and install it via the ansible-galaxy command
```
- src: git+https://github.com/polster/ansible-nessus-agent.git
  name: "nessus-agent"
  version: "v1.0.0"
```
* Add the following line to your Ansible playbook's role section as follows (sample):
```
roles:
    - role: nessus-agent
```

### Deploy and pair

* Pass in the following values in order to deploy and link the agent (sample values):
```
roles:
    - role: nessus-agent
      nessus_agent_version: "6.9.1"
      nessus_agent_key: "sdfasdjfee4545345345gasdgsag"
      nessus_agent_name: "osx-server01.tinkerstest.com"
      nessus_agent_host_name: "nessus-manager.tinkerstest.com"
      nessus_agent_host_port: "443"
      nessus_agent_link: true
```

### Custom download location

* Being recommended to manually download the Agent installer and provide it to this role for download on an internal web server (see [known issues](#knownIssuesAgentDownload)) you need to maintain the following URL structure:
```
http(s)://<host or ip>/path/NessusAgent-<version>.dmg
```
* Use the overridable default var in order to point the Ansible role to the new download location (sample):
```
roles:
    - role: nessus-agent
      nessus_agent_version: "6.9.1"
      nessus_agent_download_url: "http://mywebserver.example.com/new/location/NessusAgent-6.9.1.dmg"
```

### Installed version

* As soon as the Agent has been installed, this role will create a separate version file containing the exact version of the Agent for reference
* The version file can be found here:
```
/Library/NessusAgent/
```

## Configuration

### <a name="configVariables"></a>Configurable variables

See [defaults](defaults/main.yml)

## Known issues

### <a name="knownIssuesAgentDownload"></a>Agent download url

Unfortunately the t&m confirmation parameter as part of the vendor download URL for the agent changes from time to time, so an alternative may be to simply download the needed Agent version manually and then put the same on an internal web server.
