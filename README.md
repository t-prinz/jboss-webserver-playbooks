# Ansible playbooks for Red Hat JBoss Web Server (JWS)

These playbooks can be used to install JWS and deploy a sample application.

### Prerequisites

1.  The target system needs to be running RHEL 7 or 8.
2.  The target system needs to be registered (to the Red Hat portal or to Satellite) and have access to the JWS repositories.

### Using the playbooks

The following workflow shows how these playbooks can be used to set up a Satellite server.

    ansible-playbook -i inventory \
                     -l host.my.domain \
                     install_jws.yml

    ansible-playbook -i inventory \
                     -l host.my.domain \
                     install_app.yml

Once the application has been installed, it can be accessed at

    http://host.my.domain:8080/HelloServlet-1.0.0
