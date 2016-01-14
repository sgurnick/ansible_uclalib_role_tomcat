# UCLALib Ansible Role: Tomcat

Installs Tomcat on RHEL servers

A top-level Tomcat CATALINA_HOME is installed with separate CATALINE_BASEs for each application

## Variables

  tomcat_major_version - defines the major version of Tomcat to use (e.g. 6, 7, 8, etc.)

  tomcat_version - defines the full version of tomcat to use (e.g. 7.0.67)

  tomcat_applications - defines the application name, shutdown port, and connector port for each application

  Sample format:
  ```
  tomcat_applications:
    - app_name: app1
      shut_port: 8006
      conn_port: 8081
      rproxy_path: path1
    - app_name: app2
      shut_port: 8007
      conn_port: 8082
      rproxy_path: path2
  ```
  This variables definition should be placed in an external var files and included in a playbook using the vars_files statement:
  Example:
  ```
  ---
  - name: uclalib_tomcat_param.yml
    sudo: true
    hosts: test
    vars_files:
      - plays_vars/tomcat_app_vars.yml

    roles:
      - { role: uclalib_role_java }
      - { role: uclalib_role_apache }
      - { role: uclalib_role_tomcat }
  ```

  tomcat_server_name - defines the FQDN for the server the tomcat apps will run on. This is used when creating the HTTPD vhost configuration

  tomcat_subdirs - defines the sub-directories to create in each CATALINE_BASE app directory

  default_webapps - defines the default tomcat webapps that will be removed
