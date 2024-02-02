# ansible-rol-CCN-STIC-619B

Este proyecto tiene como objetivo traducir los scripts que acompañan a la guía CN-STIC-619B a Ansible. No se trata de que desde Ansible se copie el script correspondiente y se ejecute, sino de traducir la funcionalidad a la estructura de Ansible, definiendo el estado final en el que ha de quedar el sistema, comprobando si se cumple o no, y realizar las acciones correctivas correspondientes.

## Cómo contribuir

Descarga este repositorio, crea una rama con los cambios a introducir y pide un PR (Pull Request) a, al menos, uno de los colaboradores para que verifique los cambios antes de integrarlos en el repositorio.

Recuerda que este rol de Ansible pretende seguir fielmente lo indicado en la guía y en el ENS, por lo que no propongas cambios que estén fuera de este marco. Tampoco se han de introducir cambios personalizados a un organismo en concreto. Para esto último se puede realizar un fork del repositorio e introducir en él esos cambios ad-hoc.

Los playbooks de Ansible deben estar preparados para ser lanzados periódicamente desde AWX, por ejemplo, al contrario que los scripts que están pensados para ser lanzados una única vez. Ten en cuenta esto al crear las tareas de los playbooks.

[Ansible-lint](https://ansible-lint.readthedocs.io/) es una herramienta que ayuda a que los playbooks creados sigan patrones y buenas prácticas de diseño. Úsala para verificar que los playbooks que creas sigan estas buenas prácticas.

## Cómo usar el rol

1. Descarga el código del repositorio dentro de una carpeta dentro del directorio roles donde tengas la instalación de Ansible.
2. Crea un playbook que incluya el rol.
3. Ejecuta el playbook contra el inventario a bastionar indicando la etiqueta en función del nivel de categoría ENS:
   1. ens_basica
   2. ens_media
   3. ens_alta

Hay que tener en cuenta que el rol necesita de variables que han de ser definidas por quien vaya a ejecutar el playbook:
* ansible_ssh_private_key. Indica la clave a usar para conectarse con cada servidor.
* grub_root_pass. La contraseña de ususario root a configurar en grub. Se recomienda que esa contraseña se almacene encriptada haciendo uso de Ansible Vault.
* root_pass. La contraseña del usuario root de cada máquina. El rol forzará el cambio de contraseña de root si no se cumplen los parámetros de seguridad indicados por la guía y si, en base a ellos, la contraseña estuviera caducada.

A la hora de ejecutar el rol habrá que indicar el nivel de categoría del ENS que han de cumplir los hosts donde se aplicará el bastionado. Ejemplo:

```bash
ansible-playbook my_playbook_con_rol_CCN-STIC-619B.yml -i hosts_categoria_media_ENS --tag ens_media
```
Habrá que añadir otras etiquetas en la ejecución del rol en los siguientes casos:
* `gnome`. En el caso de que el sistema de escritorio esté instalado.
* `portatiles`. En el caso de que se trate de un equipo portátil.

Ejemplo:
```bash
ansible-playbook my_playbook_con_rol_CCN-STIC-619B.yml -i hosts_categoria_media_ENS --tag ens_media,gnome,portatiles
```
