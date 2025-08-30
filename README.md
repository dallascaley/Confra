The following is the result of me asking the roboot, "why do we have all these folders?"

🔹 group_vars/

  Purpose:
    This directory contains variable files that are automatically loaded based on the group names defined in your inventory.

  Why it exists:
    Ansible organizes hosts into groups (e.g., webservers, dbservers, production, etc.). You often want to define configuration variables that apply to all hosts in a group, and group_vars/ is where you do that.

  Example structure:

    group_vars/
      all.yml            # Variables applied to all hosts
      webservers.yml     # Variables just for the webservers group
      dbservers.yml      # Variables just for the dbservers group


  Automatically loaded:
  Ansible automatically looks in this folder when a group is referenced in your inventory.

🔹 inventory/

  Purpose:
    This is where you define your inventory of hosts — the systems you want to manage.

  Why it exists:
    Ansible needs to know what machines to connect to, how to connect, and how they are grouped. The inventory/ folder allows for organizing this info, especially in larger projects or multi-environment setups.

  Example structure:

    inventory/
      hosts               # A static inventory file
      dev/hosts           # Environment-specific inventory
      prod/hosts


  You can structure inventory files however you like — flat or nested — and they can be static (ini, yaml) or dynamic (scripts, plugins).

🔹 playbooks/

  Purpose:
    This folder holds your Ansible playbooks, which define what tasks to run and where to run them.

  Why it exists:
    Playbooks are the heart of Ansible: YAML files that orchestrate configuration, deployment, and orchestration tasks. Keeping them in their own folder helps keep things modular and clean.

  Example structure:

    playbooks/
      deploy_web.yml
      install_db.yml
      site.yml              # Could be the main entry point playbook


  You might also see subfolders like tasks/ or handlers/ here, but those are more commonly found in the roles/ structure.

🔹 roles/

  Purpose:
    Roles are a way to group related tasks, variables, handlers, templates, and files into reusable components.

  Why it exists:
    Roles enforce best practices for organizing complex playbooks and encourage reusability and modularity.

  Structure of a role (within the roles/ folder):

    roles/
      nginx/
        tasks/
          main.yml
        templates/
          nginx.conf.j2
        vars/
          main.yml
        handlers/
          main.yml
        defaults/
          main.yml
        files/
        meta/


  Each role is self-contained. If you have multiple playbooks needing to configure NGINX, for example, you can just include_role: nginx in each.

Why This Structure is Common

  This layout is:

    * Scalable — handles environments, multiple playbooks, reusable roles

    * Discoverable — easy to see what hosts, vars, and roles exist

    * Compliant — follows Ansible best practices and community standards

  You don't have to organize your Ansible project this way, but doing so:

    * Makes it easier to maintain and collaborate

    * Reduces duplication

    * Leverages Ansible’s automatic variable loading and file resolution