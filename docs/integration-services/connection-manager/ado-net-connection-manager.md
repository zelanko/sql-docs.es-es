---
title: Administrador de conexiones ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 32b01cce82cd1fd2af018b002a3c551ea480c000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897992"
---
# <a name="adonet-connection-manager"></a>Administrador de conexiones ADO.NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite a un paquete tener acceso a orígenes de datos mediante un proveedor .NET. Este administrador de conexiones normalmente se usa para acceder a orígenes de datos como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como a orígenes de datos expuestos a través de OLE DB y XML en tareas personalizadas que se escriben en código administrado con un lenguaje como C#.  
  
 Cuando agrega un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a un paquete, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **ADO.NET**. El valor de **ConnectionManagerType** se califica para incluir el nombre del proveedor .NET que usa el administrador de conexiones.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solución de problemas del administrador de conexiones ADO.NET  
 Puede registrar las llamadas realizadas por el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] establece con orígenes de datos externos. Para registrar las llamadas que el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] realiza a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Al ser leídos por un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , los datos de ciertos tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generarán los resultados que se muestran en la tabla siguiente.  
  
|Tipo de datos de SQL Server|Resultado|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|Se produce un error en el paquete a menos que el paquete utilice comandos SQL parametrizados. Para utilizar comandos SQL parametrizados, utilice la tarea Ejecute SQL en el paquete. Para más información, vea [Tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|El administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] trunca el valor de milisegundos.|  
  
> [!NOTE]  
>  Para más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) y [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configuración del administrador de conexiones ADO.NET  
 Puede configurar el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] de las maneras siguientes:  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
-   Proporcionar una cadena de conexión específica configurada para cumplir con los requisitos del proveedor .NET seleccionado.  
  
-   Según el proveedor, incluir el nombre del origen de datos al cual conectarse.  
  
-   Proporcionar credenciales de seguridad según resulte apropiado para el proveedor seleccionado.  
  
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.  
  
 Muchas de las opciones de configuración del administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dependen del proveedor .NET que usa el administrador de conexiones.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Configurar el administrador de conexiones ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="configure-adonet-connection-manager"></a>Configurar el administrador de conexiones ADO.NET
  Utilice el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** para agregar una conexión a un origen de datos al que se puede tener acceso mediante un proveedor de datos de .NET Framework, como el proveedor SqlClient. El administrador de conexiones puede utilizar una conexión existente o puede crear una nueva.  
  
 Para obtener más información acerca del administrador de conexiones ADO .NET, vea [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Conexiones de datos**  
 Seleccione una conexión de datos ADO.NET de la lista.  
  
 **Propiedades de conexión de datos**  
 Vea las propiedades y los valores de la conexión de datos ADO.NET seleccionada.  
  
 **Nueva**  
 Cree una conexión de datos ADO.NET mediante el cuadro de diálogo **Administrador de conexiones** .  
  
 **Eliminar**  
 Seleccione una conexión y elimínela con el botón **Eliminar** .  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Identidades administradas para la autenticación de los recursos de Azure
Al ejecutar paquetes SSIS en el [entorno de ejecución de integración de Azure-SSIS en Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), puede usar la [identidad administrada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) asociada a su factoría de datos para la autenticación en Azure SQL Database (o en la instancia administrada). Puede acceder a la factoría designada y copiar datos desde la base de datos o en la base de datos usando esta identidad.

Para usar la autenticación de la identidad administrada en Azure SQL Database, siga estos pasos para configurar la base de datos:

1. **Cree un grupo en Azure AD**. Convierta la identidad administrada en miembro del grupo.
    
   1. [Busque la identidad administrada de la factoría de datos en Azure Portal](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Vaya a **Propiedades** en la factoría de datos. Copie el **Id. del objeto de identidad administrada**.
    
   1. Instale el módulo de [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2). Inicie sesión con el comando `Connect-AzureAD`. Ejecute los comandos siguientes para crear un grupo y agregue la identidad administrada como miembro.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. **[Aprovisione un administrador de Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** para Azure SQL Server en Azure Portal si aún no lo ha hecho. El administrador de Azure AD puede ser un usuario o un grupo de Azure AD. Si concede un rol de administrador al grupo con identidad administrada, omita los pasos 3 y 4. El administrador tendrá acceso completo a la base de datos.

1. **[Cree usuarios de base de datos independiente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** para el grupo de Azure AD. Conéctese a la base de datos en la que va a copiar o pegar datos mediante herramientas como SSMS, con una identidad de Azure AD que tenga al menos el permiso ALTER ANY USER. Ejecute el T-SQL siguiente: 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. **Conceda los permisos necesarios al grupo de Azure AD** como lo haría normalmente para los usuarios de SQL y otros. Por ejemplo, ejecute el siguiente código:

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

Para usar la autenticación de la identidad administrada en la instancia administrada de Azure SQL Database, siga estos pasos para configurar la base de datos:
    
1. **[Aprovisione un administrador de Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** para la instancia administrada en Azure Portal si aún no lo ha hecho. El administrador de Azure AD puede ser un usuario o un grupo de Azure AD. Si concede un rol de administrador al grupo con identidad administrada, omita los pasos 2-5. El administrador tendrá acceso completo a la base de datos.

1. **[Busque la identidad administrada de la factoría de datos en Azure Portal](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Vaya a **Propiedades** en la factoría de datos. Copie el **Id. de la aplicación de identidad administrada** (NO el **Id. del objeto de identidad administrada**).

1. **Convierta la identidad administrada de la factoría de datos al tipo binario**. Conéctese a la base de datos **maestra** de su instancia administrada con herramientas como SSMS, desde su cuenta de administrador de SQL o Active Directory. Ejecute el siguiente comando T-SQL en la base de datos **maestra** para obtener el Id. de la aplicación de identidad administrada como un binario:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. **Agregue la identidad administrada de la factoría de datos como usuario** en la instancia administrada de Azure SQL Database. Ejecute el siguiente comando T-SQL en la base de datos **maestra**:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **Conceda los permisos necesarios a la identidad administrada de la factoría de datos**. Ejecute el siguiente comando T-SQL en la base de datos en la que va a copiar o pegar datos:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

Por último, **configure la autenticación de la identidad administrada** para el administrador de conexiones ADO.NET. Tiene dos opciones para hacerlo:
    
1. Configurarla durante su diseño. En el Diseñador SSIS, haga clic en el administrador de conexiones ADO.NET y haga clic en **Propiedades** para abrir la ventana **Propiedades**. Actualice la propiedad **ConnectUsingManagedIdentity** en **true**.
    > [!NOTE]
    >  Actualmente, la propiedad del administrador de conexiones **ConnectUsingManagedIdentity** NO surte efecto (lo que indica que la autenticación de la identidad administrada no funciona) al ejecutar el paquete SSIS en el Diseñador SSIS o en [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.
    
1. Configurarla durante su ejecución. Al ejecutar el paquete a través de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) o de la [actividad de paquetes para la ejecución de SSIS de Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), busque el administrador de conexiones ADO.NET y actualice su propiedad **ConnectUsingManagedIdentity** en **true**.
    > [!NOTE]
    >  En el entorno de ejecución de integración de Azure-SSIS, se **reemplazarán** todos los demás métodos de autenticación (por ejemplo, autenticación integrada, contraseña) preconfigurados en el administrador de conexiones ADO.NET cuando se use la autenticación de la identidad administrada para establecer la conexión de base de datos.

> [!NOTE]
>  Para configurar la autenticación de la identidad administrada en los paquetes existentes, vuelva a generar el proyecto de SSIS con el [Diseñador SSIS más reciente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) al menos una vez, e implemente de nuevo ese proyecto SSIS en su entorno de ejecución de integración de Azure-SSIS de modo que la nueva propiedad del administrador de conexiones **ConnectUsingManagedIdentity** se agregue automáticamente a todos los administradores de conexiones ADO.NET del proyecto de SSIS.

## <a name="see-also"></a>Consulte también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
