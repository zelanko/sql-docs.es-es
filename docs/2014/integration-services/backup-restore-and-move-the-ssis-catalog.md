---
title: Copia de seguridad, restauración y traslado del catálogo de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 314dfaee23854524884edd0fe67fe1f45ec89b2e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925276"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>Copia de seguridad, restauración y traslado del catálogo de SSIS
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] incluye la base de datos de SSISDB. En la base de datos de SSISDB, se consultan vistas para inspeccionar objetos, valores y los datos operativos que se almacenan en el catálogo de **SSISDB** , consultando las vistas de la base de datos de SSISDB. Este tema proporciona instrucciones para hacer una copia de seguridad de la base de datos y restaurarla.  
  
 El catálogo de **SSISDB** almacena los paquetes que se han implementado en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para más información sobre el catálogo, vea [Catálogo de SSIS](catalog/ssis-catalog.md).  
  
##  <a name="to-back-up-the-ssis-database"></a><a name="backup"></a>Para realizar una copia de seguridad de la base de datos de SSIS  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
2.  Para realizar una copia de seguridad de la clave maestra de la base de datos de SSISDB, use la instrucción Transact-SQL BACKUP MASTER KEY. La clave se almacena en un archivo que especifique. Use una contraseña utilizada para cifrar la clave maestra del archivo.  
  
     Para más información sobre la instrucción, vea [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
     En el ejemplo siguiente, la clave maestra se exporta al archivo `c:\temp directory\RCTestInstKey` . La contraseña de `LS2Setup!` se usa para cifrar la clave maestra.  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  Use el cuadro de diálogo **Copia de seguridad de la base de datos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para realizar una copia de seguridad de la base de datos de SSISDB. Para más información, vea [Cómo realizar una copia de seguridad de una base de datos (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812).  
  
4.  Realice el procedimiento siguiente para generar el script CREATE LOGIN para ##MS_SSISServerCleanupJobLogin##. Para obtener más información, vea [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
    1.  En el Explorador de objetos de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda el nodo **Seguridad** y el nodo **Inicios de sesión** .  
  
    2.  Haga clic con el botón derecho en **##MS_SSISServerCleanupJobLogin##** y, después, haga clic en **Incluir inicio de sesión como** > **CREATE To** > **Nueva ventana del Editor de consultas**.  
  
5.  Si restaura la base de datos de SSISDB a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que nunca se ha creado el catálogo de SSISDB, genere el script CREATE PROCEDURE para sp_ssis_startup como se indica aquí. Para obtener más información, vea [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
    1.  En explorador de objetos, expanda el nodo **bases de datos** y, a continuación, expanda el nodo **bases de datos del sistema**y  >  **master**  >  **Programmability**  >  **procedimientos almacenados** de programación maestra.  
  
    2.  Haga clic con el botón derecho en **dbo.sp_ssis_startup**y, después, haga clic en **Incluir procedimiento almacenado como** > **CREATE To** > **Nueva ventana del Editor de consultas**.  
  
6.  Confirme que se ha iniciado el Agente SQL Server  
  
7.  Si restaura la base de datos de SSISDB a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde el catálogo de SSISDB nunca se creó, genere un script para el trabajo de mantenimiento de SSIS Server. como se indica a continuación. El script se crea en el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] automáticamente cuando se crea el catálogo de SSISDB. El trabajo sirve de ayuda para limpiar los registros de operación de la limpieza fuera de la ventana de retención y para eliminar versiones anteriores de proyectos.  
  
    1.  En el Explorador de objetos, expanda el nodo **Agente SQL Server** y luego expanda el nodo **Trabajos** .  
  
    2.  Haga clic con el botón secundario en trabajo de mantenimiento del servidor SSIS y, a continuación, haga clic en **incluir trabajo como**  >  **crear en**  >  **nueva ventana del editor de consultas**.  
  
### <a name="to-restore-the-ssis-database"></a>Para restaurar la base de datos de SSIS  
  
1.  Si va a restaurar la base de datos de SSISDB en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que el catálogo de SSISDB nunca se creó, habilite Common Language Runtime (CLR) ejecutando el procedimiento almacenado sp_configure. Para más información, vea [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) y [clr enabled (opción)](https://go.microsoft.com/fwlink/?LinkId=231855).  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  Si va a restaurar la base de datos de SSISDB a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que el catálogo de SSISDB nunca se creó, cree la clave asimétrica y el inicio de sesión de la clave asimétrica y conceda el permiso UNSAFE al inicio de sesión.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] requieren permisos UNSAFE para el inicio de sesión porque este debe disponer de acceso adicional con el fin de restringir recursos como, por ejemplo la API Win32 de Microsoft. Para obtener más información sobre el permiso de código UNSAFE, vea [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  Use el cuadro de diálogo **Restaurar base de datos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]para restaurar la base de datos de SSISDB a partir de una copia de seguridad. Para obtener más información, vea los temas siguientes:  
  
    -   [Restaurar la base de datos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)  
  
    -   [Restaurar base de datos &#40;página Archivos&#41;](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [Restaurar base de datos &#40;página Opciones&#41;](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  Ejecute los scripts que ha creado en [Para realizar una copia de seguridad de la base de datos de SSIS](#backup) para ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup y el trabajo de mantenimiento del servidor de SSIS. Confirme que se ha iniciado el Agente SQL Server.  
  
5.  Ejecute la instrucción siguiente con el fin de establecer el procedimiento de sp_ssis_startup para que se ejecute automáticamente. Para más información, vea [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql).  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  Asigne el usuario de SSISDB ##MS_SSISServerCleanupJobUser## (base de datos de SSISDB) a ##MS_SSISServerCleanupJobLogin## (para hacerlo, use el cuadro de diálogo **Propiedades de inicio de sesión** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]).  
  
7.  Restaure la clave maestra mediante uno de los métodos siguientes. Para obtener más información acerca del cifrado, vea [Encryption Hierarchy](../relational-databases/security/encryption/encryption-hierarchy.md).  
  
    -   **Método 1**  
  
         Use este método si ya ha realizado una copia de seguridad de la clave maestra de la base de datos y dispone de la contraseña que se utilizó para cifrar la clave maestra.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  Confirme que la cuenta de servicio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene permisos para leer el archivo de la clave de la copia de seguridad.  
  
        > [!NOTE]  
        >  Aparecerá el mensaje de advertencia siguiente que se muestra en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] si la clave maestra de la base de datos no se ha cifrado aún con la clave maestra de servicio. Omita el mensaje de advertencia.  
        >   
        >  **No se puede descifrar la clave maestra actual. Se omitió el error porque se especificó la opción FORCE.**  
        >   
        >  El argumento FORCE especifica que el proceso de restauración debe continuar aunque la clave maestra de la base de datos actual no está abierta. Dado que la clave maestra de la base de datos no se ha abierto aún en la instancia donde se están restaurando la base de datos, aparecerá este mensaje para el catálogo de SSISDB.  
  
    -   **Método 2**  
  
         Use este método si tiene la contraseña original que se usó para crear SSISDB.  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  Determine si el esquema del catálogo de SSISDB y los binarios de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (ensamblado de ISServerExec y SQLCLR) son compatibles (para hacerlo, ejecute [catalog.check_schema_version](/sql/integration-services/system-stored-procedures/catalog-check-schema-version)).  
  
9. Para confirmar que la base de datos de SSISDB se ha restaurado correctamente, realice operaciones sobre el catálogo de SSISDB como, por ejemplo, ejecutar paquetes que se hayan implementado en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para más información, vea [Ejecutar un paquete en el Servidor SSIS con SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md).  
  
### <a name="to-move-the-ssis-database"></a>Para mover la base de datos de SSIS  
  
-   Siga las instrucciones para mover las bases de datos de usuarios. Para más información, consulte [Move User Databases](../relational-databases/databases/move-user-databases.md).  
  
     Asegúrese de realizar una copia de seguridad de la clave maestra de la base de datos de SSISDB y de proteger el archivo de copia de seguridad. Para más información, vea [Para realizar una copia de seguridad de la base de datos de SSIS](#backup).  
  
     Asegúrese de que los objetos correspondientes de Integration Services (SSIS) se han creado en la nueva instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde aún no se haya creado el catálogo de SSISDB.  
  
  
