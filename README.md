# Ansible playbooks for Red Hat JBoss Web Server (JWS)

These playbooks can be used to install JWS on a RHEL system and deploy a sample application.

### Prerequisites

* The target system needs to be running RHEL 7 or RHEL 8.
* If using the RPM installation method, the target system needs to be registered (to the Red Hat portal or to Satellite) and have access to the JWS repositories.  The correct repositories will be enabled during installation.
* If using the zip installation method, the JWS zip files must be downloaded locally from the Red Hat portal.

        jws-5.5.0-application-server.zip
        jws-5.5.0-application-server-RHEL8-x86_64.zip

### Using the playbooks

Decide on an installation method (RPM or zip) and run the appropriate playbooks:

For a RPM installation:

    ansible-playbook -i inventory \
                     -l host.my.domain \
                     install_jws.yml

    ansible-playbook -i inventory \
                     -e jws_app_dir=/opt/rh/jws5/root/usr/share/tomcat/webapps \
                     -l host.my.domain \
                     install_app.yml

For a zip installation:

    ansible-playbook -i inventory \
                     -e jboss_jws_zip_file=your-dir-path/jws-5.5.0-application-server.zip \
                     -e jboss_jws_zip_platform_arch_file=your-dir-path/jws-5.5.0-application-server-RHEL8-x86_64.zip \
                     -l host.my.domain \
                     install_jws_zip.yml

    ansible-playbook -i inventory \
                     -e jws_app_dir=/opt/jws-5.5/tomcat/webapps \
                     -l host.my.domain \
                     install_app.yml

Once JWS has been installed, the splash page can be accessed at the following location.  Note that the various links on the page will not work, which is normal.

    http://host.my.domain:8080

Once the application has been installed, it can be accessed at

    http://host.my.domain:8080/HelloServlet-1.0.0

The `install_app.yml` playbook uses git to copy a repository that has a pre-built artifact in the `target` directory.  The git repository and artifact can be specified via variables:

    ansible-playbook -i inventory \
                     -e git_app_repo=https://github.com/the-repo.git \
                     -e jws_war_name=war_file \
                     -e jws_app_dir=/opt/jws-5.5/tomcat/webapps \
                     -l host.my.domain \
                     install_app.yml
