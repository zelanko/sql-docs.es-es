---
title: Administrador de conexiones OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c455e449ff59296848c7e3f15d07aaee80d415c7
ms.sourcegitcommit: e92ce0f59345fe61c0dd3bfe495ef4b1de469d4b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2019
ms.locfileid: "66221156"
---
# <a name="ole-db-connection-manager"></a>OLE DB, administrador de conexiones

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Un administrador de conexiones OLE DB permite a un paquete conectarse a un origen de datos mediante un proveedor OLE DB. Por ejemplo, un administrador de conexiones OLE DB que se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar el proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 no admite las nuevas palabras clave de cadena de conexión (MultiSubnetFailover=True) para la agrupación en clústeres de conmutación por error de varias subredes. Para obtener más información, vea las [Notas de la versión de SQL Server](https://go.microsoft.com/fwlink/?LinkId=247824) y la entrada de blog [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)(Clúster de conmutación de varias subredes y SSIS de AlwaysOn), en www.mattmasson.com.    
> 
> [!NOTE]
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, el origen de datos requiere un proveedor de datos distinto al de las versiones anteriores de Excel o Access. Para obtener más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) y [Conectarse a una base de datos de Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 Varias tareas y componentes de flujo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan un administrador de conexiones OLE DB. Por ejemplo, un origen de OLE DB y un destino de OLE DB usan este administrador de conexiones para extraer y cargar datos, y la tarea Ejecutar SQL puede usar este administrador de conexiones para conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar consultas.    
    
 El administrador de conexiones OLE DB también se usa para obtener acceso a orígenes de datos OLE DB en tareas personalizadas escritas en código no administrado que usa un lenguaje como, por ejemplo, C++.    
    
 Cuando agrega un administrador de conexiones OLE DB a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se resuelve como una conexión OLE DB en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Connections** del paquete.    
    
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **OLEDB**.    
    
 El administrador de conexiones OLE DB se puede configurar de las maneras siguientes:    
    
-   Proporcionar una cadena de conexión específica configurada para cumplir con los requisitos del proveedor seleccionado.    
    
-   Según el proveedor, incluir el nombre del origen de datos al cual conectarse.    
    
-   Proporcionar credenciales de seguridad según resulte apropiado para el proveedor seleccionado.    
    
-   Indicar si la conexión creada desde el administrador de conexiones se conserva en el tiempo de ejecución.    
    
## <a name="logging"></a>Registro    
 Puede registrar las llamadas realizadas por el administrador de conexiones OLE DB a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con las conexiones que el administrador de conexiones OLE DB establece con orígenes de datos externos. Para registrar las llamadas que el administrador de conexiones OLE DB realiza a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Configuración del administrador de conexiones OLE DB    
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación. Para obtener más información sobre las propiedades que puede configurar en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea la documentación de la clase **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** en la Guía del desarrollador.    
    
## <a name="related-content"></a>Contenido relacionado    
    
-   Artículo wiki, sobre [SSIS con conectores Oracle](https://go.microsoft.com/fwlink/?LinkId=220670) en social.technet.microsoft.com.    
    
-   Artículo técnico, sobre [cadenas de conexión para proveedores OLE DB](https://go.microsoft.com/fwlink/?LinkId=220744), en carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>Configurar el administrador de conexiones OLE DB
  Utilice el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** para agregar una conexión a un origen de datos; puede ser una nueva conexión o una copia de una conexión existente.  
  
> [!NOTE]  
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, el origen de datos requiere un administrador de conexiones distinto al de las versiones anteriores de Excel. Para más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, el origen de datos requiere un proveedor OLE DB diferente que las versiones anteriores de Access. Para más información, vea [Conectarse a una base de datos de Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Para obtener más información acerca del administrador de conexiones OLE DB, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Conexiones de datos**  
 Seleccione en la lista una conexión de datos OLE DB existente.  
  
 **Propiedades de conexión de datos**  
 Vea las propiedades y los valores de la conexión de datos OLE DB seleccionada.  
  
 **Nueva**  
 Permite crear una conexión de datos OLE DB con el cuadro de diálogo **Administrador de conexiones** .  
  
 **Eliminar**  
 Permite seleccionar una conexión de datos y, después, eliminarla con el botón **Eliminar** .  
  
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

Después, **configure el proveedor OLE DB** para el administrador de conexiones OLE DB. Tiene dos opciones para hacerlo:
    
1. Configurarla durante su diseño. En el Diseñador SSIS, haga doble clic en el administrador de conexiones OLE DB para abrir la ventana del **administrador de conexiones**. En la lista desplegable **Proveedor**, seleccione [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  Puede ser que otros proveedores de la lista desplegable NO admitan la autenticación de la identidad administrada.
    
1. Configurarla durante su ejecución. Cuando ejecute el paquete a través de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) o de la [actividad del paquete SSIS de Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), busque la propiedad del administrador de conexiones **ConnectionString**  para el administrador de conexiones OLE DB y actualice la propiedad de conexión **Provider** a **MSOLEDBSQL** (es decir, Microsoft OLE DB Driver for SQL Server).
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Por último, **configure la autenticación de la identidad administrada** para el administrador de conexiones OLE DB. Tiene dos opciones para hacerlo:
    
1. Configurarla durante su diseño. En el Diseñador SSIS, haga clic en el administrador de conexiones OLE DB y haga clic en **Propiedades** para abrir la ventana **Propiedades**. Actualice la propiedad **ConnectUsingManagedIdentity** en **true**.
    > [!NOTE]
    >  Actualmente, la propiedad del administrador de conexiones **ConnectUsingManagedIdentity** NO surte efecto (lo que indica que la autenticación de la identidad administrada no funciona) al ejecutar el paquete SSIS en el Diseñador SSIS o en [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.

1. Configurarla durante su ejecución. Al ejecutar el paquete a través de la actividad SSMS o al ejecutar la actividad del paquete de SQL, busque el administrador de conexiones OLE DB y actualice su propiedad **ConnectUsingManagedIdentity** en **true**.
    > [!NOTE]
    >  En el entorno de ejecución de integración de Azure-SSIS, se **reemplazarán** todos los demás métodos de autenticación (por ejemplo, seguridad integrada, contraseña) preconfigurados en el administrador de conexiones OLE DB cuando se use la autenticación de la identidad administrada para establecer la conexión de base de datos.

> [!NOTE]
>  Para configurar la autenticación de la identidad administrada en los paquetes existentes, vuelva a generar el proyecto de SSIS con el [Diseñador SSIS más reciente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) al menos una vez, e implemente de nuevo ese proyecto SSIS en su entorno de ejecución de integración de Azure-SSIS de modo que la nueva propiedad del administrador de conexiones **ConnectUsingManagedIdentity** se agregue automáticamente a todos los administradores de conexiones OLE DB del proyecto de SSIS.

## <a name="see-also"></a>Consulte también    
 [Origen de OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destino de OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
