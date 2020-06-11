---
title: Instalación de componentes de SSMA en SQL Server (OracleToSQL) | Microsoft Docs
description: Obtenga información acerca de cómo instalar el paquete de extensión de SSMA y los proveedores de Oracle en el equipo que ejecuta SQL Server para admitir la conversión de bases de datos de Oracle.
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 3df476f5fa14840af0b023253b79702ed7a85c8a
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292939"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalación de componentes de SSMA en SQL Server (OracleToSQL)

Además de instalar SSMA, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Estos componentes incluyen el paquete de extensión SSMA, que admite la migración de datos y los proveedores de Oracle para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA para Oracle Extension Pack

El paquete de extensión SSMA agrega las bases de datos **sysdb** y **ssmatesterdb** a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La base de datos **sysdb** contiene las tablas y los procedimientos almacenados necesarios para migrar los datos y las funciones definidas por el usuario que emulan las funciones del sistema de Oracle. La base de datos **ssmatesterdb** contiene las tablas y los procedimientos necesarios para el componente Tester.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente cuando se usa el motor de migración de datos del lado servidor para migrar los datos.  
  
### <a name="prerequisites"></a>Requisitos previos

Antes de instalar SSMA para los componentes de servidor de Oracle en, asegúrese de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el sistema cumple los requisitos siguientes:  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la instancia de está instalada. SSMA no es compatible con SQL Server 2008 Express Edition.
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
- El proveedor de cliente de Oracle o el proveedor de OLE DB para Oracle y la conectividad a la base de datos de Oracle que desea migrar. Puede instalar proveedores desde el sitio web de Oracle u Oracle.  
  
- El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser debe estar en ejecución durante la instalación. Se utiliza para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Asistente para la instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio explorador de se está ejecutando, pero todavía no ve una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar el Firewall de Windows para desbloquear temporalmente el puerto o puede deshabilitar temporalmente el Firewall de Windows. Es posible que también tenga que deshabilitar temporalmente el software antivirus. Asegúrese de habilitar los firewalls y el software antivirus después de la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalación del paquete de extensión

Puede instalar el paquete de extensión en cualquier momento antes de migrar los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro del rol de servidor **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Para instalar el paquete de extensión**
  
1. Si no lo ha hecho ya, extraiga todos los archivos del archivo zip de SSMA.  
  
    Dependiendo de la versión de WinZip que tenga, puede hacer doble clic en el archivo, o bien hacer clic con el botón secundario en el archivo y, a continuación, seleccionar **extraer todo** o **abrir en WinZip**. Siga las instrucciones de la interfaz de usuario de WinZip para extraer los archivos.  
  
2. Copie **SSMA para Oracle Extension Pack.* n*.Install.exe** (donde *n* es el número de compilación) al equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3. Haga doble clic en **SSMA para Oracle Extension Pack.* n*.Install.exe**.  
  
4. En la página **principal**, seleccione **Siguiente**.  
  
5. En la página contrato de licencia para el **usuario final** , lea el contrato de licencia. Si está de acuerdo, active la casilla acepto **los términos del contrato de licencia** y, después, seleccione **siguiente**.  
  
6. En la página **elegir tipo de instalación** , seleccione **típica**.  
  
7. En la página **listo para instalar** , seleccione **instalar**.  
  
8. En la página **finalización del primer paso de la instalación** , seleccione **siguiente**.  
  
    Aparecerá un nuevo cuadro de diálogo en el que podrá seleccionar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
9. Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que va a migrar los esquemas de Oracle y, después, seleccione **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Las instancias con nombre van seguidas de una barra diagonal inversa y el nombre de la instancia.  
  
10. En la página conexión, seleccione el método de autenticación y, después, seleccione **siguiente**.  
  
    La autenticación de Windows usará sus credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y una contraseña.  
  
11. En la página siguiente, seleccione **instalar Utilities Database** *n*, donde *n* es el número de versión y, después, seleccione **siguiente**.  
  
    La base de datos **sysdb** se crea y se crean las funciones definidas por el usuario y los procedimientos almacenados en esa base de datos.  
  
    Si la opción **instalar base de datos de prueba** está activada, se creará la base de datos de **ssmatesterdb** de evaluador.  
  
12. Para instalar las utilidades en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **sí**y, después, haga clic en **siguiente**, o bien, para salir del asistente, seleccione **no**.  
  
13. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la utilidad SQLCMD, ejecute el siguiente script para habilitar CLR:  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    Si CLR no está habilitado, recibirá el siguiente error cuando SSMA se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    SSMA no pudo recuperar la información de versión del ensamblado del paquete de extensión. Vuelva a instalar el paquete de extensión en el servidor de base de datos.  
  
### <a name="sql-server-database-objects"></a>SQL Server objetos de base de datos  

Después de instalar el paquete de extensión, aparece una tabla **ssma_oracle. bcp_migration_packages** en la base de datos **sysdb** .

Cada vez que se migran datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Estos trabajos se denominan **ssma_oracle paquete de migración de datos {GUID}** y se pueden ver en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en la carpeta trabajos.  
  
## <a name="see-also"></a>Consulte también

[Instalación de SSMA para el cliente de Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Migrar bases de datos de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
