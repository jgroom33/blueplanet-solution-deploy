Role Name
=========

An ansible role to set the solutions for a Blue Planet server.

Requirements
------------

Blue Planet

lineup.yml file

Role Variables
--------------

| Variable                               | Default                 | Comments (type)                |
| :------------------------------------- | :---------------------- | :----------------------------- |
| `blueplanet_solution_docker_type`      | gitlab                  | Type of docker registry ***    |
| `blueplanet_solution_docker_url`       | registry.blueplanet.com | url of registry                |
| `blueplanet_solution_docker_username`  | none                    | Username for the registry      |
| `blueplanet_solution_docker_password`  | none                    | Password for the registry      |
| `blueplanet_solution_lineup_file`      | ./lineup.yml            | location of lineup file        |

>  ***NOTE: Creating a Gitlab Registry Access Token
>  To configure a site to utilize the Gitlab registry, an Access Token is required.
>
>  Use a web browser to navigate the Gitlab ui and log in.
>  * Navigate to "User Setting" -> "Access Tokens"
>  * Select read_registry permissions.
>  * Click Create personal access token.
>  * Copy the resulting token. It will be included on the site's registry configuration.

Dependencies
------------

none

Example Playbook
----------------

```yml
- hosts: mdso
  gather_facts: false
  vars:
    blueplanet_solution_docker_username: "{{ lookup('env','BP_GIT_USERNAME') }}"
    blueplanet_solution_docker_password: "{{ lookup('env','BP_GIT_TOKEN') }}"
    blueplanet_solution_lineup_file: lineup.yml
  roles:
      - blueplanet-solution-deploy
```

Example lineup.yml
------------------

```yml
docker_registry:
  url: registry.blueplanet.com

platform_solution:
# registry.blueplanet.com/blueplanet/bpps/solution-platform:19.06.01
  name: platform
  vendor: blueplanet/bpps
  version: 19.06.01
application_solution:
# registry.blueplanet.com/mdso/19.06/solution-orchestrate:19.06.3-87
  name: orchestrate
  vendor: mdso/19.06
  version: 19.06.3-87
additional_solutions:
# registry.blueplanet.com/mdso/19.06/solution-orchestrate_ui:19.06.1-322
  orchestrate_ui:
    name: orchestrate_ui
    vendor: mdso/19.06
    version: 19.06.1-322
# registry.blueplanet.com/blueplanet/resourceadapters/junipermx_yang_ra/master/solution-junipermxra:1.0.0.1910
  junipermxra:
    name: junipermxra
    vendor: blueplanet/resourceadapters/junipermx_yang_ra/master
    version: 1.0.0.1910
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
