1. **En todos los servidores SQL Server, cree un inicio de sesión de servidor para Pacemaker**. La siguiente instrucción Transact-SQL crea un inicio de sesión:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   Como alternativa, puede establecer los permisos con más detalle. El inicio de sesión de Pacemaker requiere ALTER, CONTROL y VIEW DEFINITION PERMISSION para administrar el grupo de disponibilidad, así como VIEW SERVER STATE para que el inicio de sesión pueda ejecutar sp_server_diagnostics. Para obtener más información, vea [GRANT Availability Group Permissions (Transact-SQL)](http://msdn.microsoft.com/library/hh968934.aspx) [Permisos de grupo de disponibilidad GRANT (Transact_SQL)] y [sp_server_diagnostic permissions](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql#permissions) (Permisos sp_server_diagnostic).

   La siguiente instrucción Transact-SQL solo concede el permiso necesario al inicio de sesión de Pacemaker. En la instrucción siguiente, "ag1" es el nombre del grupo de disponibilidad que se agregará como recurso de clúster.

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   GRANT VIEW SERVER STATE TO pacemakerLogin
   ```

1. **En todos los servidores SQL Server, guarde las credenciales del inicio de sesión de SQL Server**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
