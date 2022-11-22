rpi-sensors-exporter
=========

Ansible role for configuration and installation of Raspberry PI sensors exporter - https://github.com/casa-delle-coccinelle/rpi-sensors-exporter/tree/master


### Role Variables

 Variable | Description | Default | Required | Versions | 
|--|--|--|--|--|
| sensors_exporter_src | Git repository URL with exporter's source | https://github.com/casa-delle-coccinelle/rpi-sensors-exporter | No | 0.0.1 |
| sensors_exporter_version | Git branch or tag with exporter's version | 0.0.1 | No | 0.0.1 |
| git_key | Git key in case of private repository | - | No | 0.0.1 |
| sensors_exporter_user_home_dir | Home directory of the exporter's user | /opt/sensors-exporter | No | 0.0.1 |
| sensors_exporter_user_name | Username of the exporter user | sensors-exporter | No | 0.0.1 |
| sensors_exporter_config_file_path | Directory path to exporter's configuration file | /etc/sensors-exporter | No | 0.0.1 |
| sensors_exporter_config_file_name | Name of exporter's configuration file | config.yaml | No | 0.0.1 |
| sensors_exporter_port | Exporter's port | 8080 | No | 0.0.1 |
| sensors_exporter_verbose_logs | If true, exporter's log level will be set to INFO | false | No | 0.0.1 |
| sensors_exporter_debug_logs | If true, exporter's log level will be set to DEBUG | false | No | 0.0.1 |
| sensors_exporter_gpio_devices_config | Configuration for GPIO sensors, connected to the system. *See example bellow* | - | No | 0.0.1 |
| sensors_exporter_ads_devices_config | Configuration for sensors, connected to ADC. *See example bellow* | - | No | 0.0.1 |


### Usage
The role can be installed using ansible-galaxy:

    ansible-galaxy install -r requirements.yaml

With the following requirements file:

    roles: 
      - name: rpi-sensors-exporter
        src: https://github.com/casa-delle-coccinelle/ansible-role-rpi-sensors-exporter.git
        version: 0.0.1

And executed with:

    ansible-playbook rpi-sensors-exporter.yaml

Bellow is example rpi-sensors-exporter.yaml playbook

### Example Playbook


    - hosts: rpi
      vars:
        sensors_exporter_port: 8081
        sensors_exporter_debug_logs: true
        sensors_exporter_ads_devices_config: |
          - name: "capacitive-v1.2"
            type: "soil_moisture"
            analog_in: 0
            max_value: 32767
            min_value: 23818
        sensors_exporter_gpio_devices_config: |
          - name: "mh-rd"
            type: "rain_drops"
            pin: 26
      roles:
         - role: rpi-sensors-exporter


**Note:** The role doesn't perform any configuration checks and sets sensors_exporter_ads_devices_config and sensors_exporter_gpio_devices_config variables as defined. If the configuration is not valid, the exporter will fail to start. For configuration requirements of the exporter, please refer to exporter's documentation - https://github.com/casa-delle-coccinelle/rpi-sensors-exporter/tree/master/docs

