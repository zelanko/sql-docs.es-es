1. **En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario y la contraseña de SQL Server para el inicio de sesión de Pacemaker**. Con el siguiente comando se crea y rellena este archivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Todos los nodos del clúster deben poder tener acceso entre sí a través de SSH**. Herramientas como hb_report o crm_report (para solucionar problemas) y explorador de historial de Hawk requieren el acceso con SSH sin contraseña entre los nodos, ya que, de lo contrario, puede que solo recopilen datos desde el nodo actual. En caso de usar un puerto de SSH no estándar, use la opción -X (vea la página man). Por ejemplo, si el puerto SSH es 3479, invoque un hb_report del siguiente modo:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Para más información, vea los [requisitos de sistema y recomendaciones en la documentación de SUSE](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Instale la extensión de alta disponibilidad**. Para instalar la extensión, siga los pasos descritos en el siguiente tema de SUSE:
    
    [Installation and Setup Quick Start](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html) (Inicio rápido de instalación y configuración)

4. **Instale el agente de recursos de FCI para SQL Server**. Ejecute los siguientes comandos en ambos nodos:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Configure automáticamente el primer nodo**. El siguiente paso consiste en configurar un clúster de un nodo en ejecución, para lo cual configuraremos el primer nodo, SLES1. Siga las instrucciones del tema de SUSE [Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) (Configurar el primer nodo).

    Cuando acabe, compruebe el estado del clúster con `crm status`:
    ```bash
    crm status
    ```

    Debe mostrar que un nodo, SLES1, está configurado.

6. **Agregue nodos a un clúster existente**. A continuación, una el nodo SLES2 al clúster. Siga las instrucciones del tema de SUSE [Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) (Agregar el segundo nodo).
    
    Cuando acabe, compruebe el estado del clúster con **crm status**. Si ha agregado el segundo nodo correctamente, el resultado debería parecerse al siguiente:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** es el recurso de clúster IP virtual que se configura durante la configuración inicial de un clúster de un nodo.

7.    **Procedimientos de eliminación**. Si necesita quitar un nodo del clúster, use el script de arranque **ha-cluster-remove**. Para más información, vea [Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap) (Información general de los scripts de arranque).  

