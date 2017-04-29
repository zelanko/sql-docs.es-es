2. En ambos nodos del clúster, cree un archivo para almacenar el nombre de usuario de SQL Server y la contraseña para el inicio de sesión de Pacemaker. El comando siguiente crea y rellena este archivo:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. En ambos nodos del clúster, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Si usa otro firewall que no tiene una configuración de alta disponibilidad integrada, deberán abrirse los puertos siguientes para que Pacemaker pueda comunicarse con otros nodos del clúster.
   >
   > * TCP: puertos 2224, 3121, 21064
   > * UDP: puerto 5405

1. Instale paquetes de Pacemaker en cada nodo.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Use la misma contraseña en ambos nodos. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Habilite e inicie el servicio `pcsd` y Pacemaker. Esto permitirá que los nodos se unan al clúster después del reinicio. Ejecute el comando siguiente en ambos nodos.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instale el agente de recursos de FCI para SQL Server. Ejecute los comandos siguientes en ambos nodos. 

   ```bash
   sudo yum install mssql-server-ha
   ```
