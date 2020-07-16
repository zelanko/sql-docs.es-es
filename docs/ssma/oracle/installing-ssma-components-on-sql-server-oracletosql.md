---
title: Instalación de componentes de SSMA en SQL Server (OracleToSQL) | Microsoft Docs
description: Obtenga información acerca de cómo instalar el paquete de extensión de SSMA y los proveedores de Oracle en el equipo que ejecuta SQL Server para admitir la conversión de bases de datos de Oracle.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 736807d427b08a1b3a32df1d295b84f4ea3d23d2
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411673"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalación de componentes de SSMA en SQL Server (OracleToSQL)

Además de instalar SSMA, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Estos componentes incluyen el paquete de extensión SSMA, que admite la migración de datos y los proveedores de Oracle para habilitar la conectividad de servidor a servidor.

## <a name="ssma-for-oracle-extension-pack"></a>SSMA para Oracle Extension Pack

El paquete de extensión SSMA agrega las bases de datos **sysdb** y **ssmatesterdb** a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La base de datos **sysdb** contiene las tablas y los procedimientos almacenados necesarios para migrar los datos y las funciones definidas por el usuario que emulan las funciones del sistema de Oracle. La base de datos **ssmatesterdb** contiene las tablas y los procedimientos necesarios para el componente Tester.

Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente cuando se usa el motor de migración de datos del lado servidor para migrar los datos.

### <a name="prerequisites"></a>Requisitos previos

Antes de instalar SSMA para los componentes de servidor de Oracle en, asegúrese de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el sistema cumple los requisitos siguientes:

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la instancia de está instalada.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.
- La [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.7.2 o una versión posterior. Puede obtenerlo en el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- El proveedor de OLE DB para Oracle (si utiliza OLE DB) y la conectividad a la base de datos de Oracle que desea migrar. Puede instalar proveedores desde el sitio web de Oracle u Oracle.
- El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser debe estar en ejecución durante la instalación. Se utiliza para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Asistente para la instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser después de la instalación.

  > [!NOTE]
  > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio explorador de se está ejecutando, pero todavía no ve una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar el Firewall de Windows para desbloquear temporalmente el puerto o puede deshabilitar temporalmente el Firewall de Windows. Es posible que también tenga que deshabilitar temporalmente el software antivirus. Asegúrese de habilitar los firewalls y el software antivirus después de la instalación.

### <a name="installing-the-extension-pack"></a>Instalación del paquete de extensión

Puede instalar el paquete de extensión en cualquier momento antes de migrar los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> Para instalar el paquete de extensión, debe ser miembro del rol de servidor **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Para instalar el paquete de extensión:

1. Copie **SSMAforOracleExtensionPack_*n*. msi** (donde *n* es el número de compilación) en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
2. Haga doble clic en **SSMAforOracleExtensionPack_*n*. msi**.
3. En la página **principal**, seleccione **Siguiente**.
4. En la página contrato de licencia para el **usuario final** , lea el contrato de licencia. Si está de acuerdo, seleccione Acepto la opción de **acuerdo** y, a continuación, haga clic en **siguiente**.
5. En la página **elegir tipo de instalación** , seleccione **típica**.
6. En la página **listo para instalar** , seleccione **instalar**.
7. En la página **finalización del primer paso de la instalación** , seleccione **siguiente**.
  
   Aparecerá un nuevo cuadro de diálogo en el que podrá seleccionar el tipo de instalación del paquete de extensión.

   instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.
  
8. Seleccione el tipo de instalación que desee y, a continuación, haga clic en **siguiente**.

   > [!IMPORTANT]
   > La opción Remote solo debe usarse al instalar el paquete de extensión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en Linux o cuando el destino es [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]las instalaciones que se ejecutan en Windows siempre deben tener instalado el paquete de extensión localmente. [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]y Azure SQL Data Warehouse no admiten el paquete de extensión.

   Si va a instalar el paquete de extensión en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia local, la página siguiente le permitirá elegir una instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que vaya a migrar los esquemas de Oracle. Elija una instancia en la lista desplegable y, a continuación, seleccione **siguiente**.

   La instancia predeterminada tiene el mismo nombre que el equipo. Las instancias con nombre van seguidas de una barra diagonal inversa y el nombre de la instancia.

9. En la página conexión, seleccione el método de autenticación y, después, seleccione **siguiente**.

   La autenticación de Windows usará sus credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona autenticación de servidor, debe especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y una contraseña.

10. El paso siguiente requiere que establezca la contraseña de una clave maestra que se usará para cifrar los datos confidenciales almacenados en la base de datos del paquete de extensión durante la migración de datos del lado servidor. Proporcione una contraseña segura y haga clic en **siguiente**.

11. En la página siguiente, seleccione **instalar las utilidades de la base de datos *n* e instalar las bibliotecas de paquetes de extensiones**, donde *n* es el número de versión. Si piensa usar la característica de evaluador, active la casilla **instalar base de datos de prueba** y, a continuación, seleccione **siguiente**.

    La base de datos **sysdb** se crea con las tablas y los procedimientos almacenados necesarios para la migración de datos (mediante el motor de migración de datos del servidor) se crean en esta base de datos.

    Si la opción **instalar base de datos de prueba** está activada, se creará la base de datos **ssmatesterdb** .

12. Una vez completada la instalación, aparecerá un mensaje preguntándole si desea instalar la base de datos de utilidades en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **sí**y, a continuación, haga clic en **siguiente**, o bien para salir del asistente, seleccione **no** y, a continuación, **salir**.

13. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la `sqlcmd` utilidad, ejecute el siguiente script para habilitar CLR:

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    Si CLR no está habilitado, recibirá el siguiente error cuando SSMA se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

    > SSMA no pudo recuperar la información de versión del ensamblado del paquete de extensión. Vuelva a instalar el paquete de extensión en el servidor de base de datos.

### <a name="sql-server-database-objects"></a>SQL Server objetos de base de datos

Después de instalar el paquete de extensión, aparece una tabla **ssma_oracle. bcp_migration_packages** en la base de datos **sysdb** .

Cada vez que se migran datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Estos trabajos se denominan **ssma_oracle paquete de migración de datos {GUID}** y se pueden ver en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en la carpeta trabajos.

## <a name="see-also"></a>Consulte también

- [Instalar SSMA para el cliente de Oracle](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [Migrar bases de datos de Oracle a SQL Server](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
