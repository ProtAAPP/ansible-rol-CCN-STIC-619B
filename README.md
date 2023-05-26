# ansible-rol-CCN-STIC-619B

Este proyecto tiene como objetivo traducir los scripts que acompañan a la guía CN-STIC-619B a Ansible. No se trata de que desde Ansible se copie el script correspondiente y se ejecute, sino de traducir la funcionalidad a la estructura de Ansible, definiendo el estado final en el que ha de quedar el sistema, comprobando si se cumple o no, y realizar las acciones correctivas correspondientes.

## Cómo contribuir

Descarga este repositorio, crea una rama con los cambios a introducir y pide un PR (Pull Request) a, al menos, uno de los colaboradores para que verifique los cambios antes de integrarlos en el repositorio.

Recuerda que este rol de Ansible pretende seguir fielmente lo indicado en la guía y en el ENS, por lo que no propongas cambios que estén fuera de este marco. Tampoco se han de introducir cambios personalizados a un organismo en concreto. Para esto último se puede realizar un fork del repositorio e introducir en él esos cambios ad-hoc.

## Cómo usar el rol

1. Descarga el código del repositorio dentro de una carpeta dentro del directorio roles donde tengas la instalación de Ansible.
2. Crea un playbook que incluya el rol.
3. Ejecuta el playbook contra el inventario a bastionar indicando la etiqueta en función del nivel de categoría ENS:
   1. ens_basica
   2. ens_media
   3. ens_alta

Hay que tener en cuenta que el rol necesita de variables que han de ser definidas por quien vaya a ejecutar el playbook:
* ansible_ssh_private_key. Indica la clave a usar para conectarse con cada servidor.
* grub_root_pass. La contraseña de ususario root a configurar en grub. Se recomienda que esa contraseña se almacene encriptada haciendo uso de Ansible Vault.

A la hora de ejecutar el rol habrá que indicar el nivel de categoría del ENS que han de cumplir los hosts donde se aplicará el bastionado. Ejemplo:

```bash
ansible-playbook my_playbook_con_rol_CCN-STIC-619B.yml -i hosts_categoria_media_ENS --tag ens_media
```