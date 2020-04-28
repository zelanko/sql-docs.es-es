---
title: Instalación de componentes de SSMA en SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029010"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalación de componentes de SSMA en SQL Server (SybaseToSQL)
Además de instalar SSMA, para usar la migración de datos del lado servidor, también debe instalar los componentes en el equipo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ejecuta. Estos componentes incluyen el paquete de extensión SSMA, que admite la migración de datos y los proveedores de Sybase para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA para el paquete de extensiones de Sybase  
El paquete de extensión SSMA agrega las bases de datos, **sysdb** y **ssmatesterdb_syb**, a la instancia especificada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de. La base de datos **sysdb** contiene las tablas y los procedimientos almacenados necesarios para migrar los datos. La base de datos de **ssmatester_syb** contiene el esquema **ssma_sybase_utilities**, en el que se crean los objetos (tablas, desencadenadores, vistas) utilizados por el componente de evaluador SSMA.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente cuando se usa el motor de migración de datos del lado servidor para migrar los datos.  
  
### <a name="installing-the-extension-pack"></a>Instalación del paquete de extensión  
Puede instalar el paquete de extensión en cualquier momento antes de migrar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos a.  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro del rol de servidor sysadmin en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar el paquete de extensión**  
  
1.  Copie SSMA para el paquete de extensión de Sybase. *n*. Instale. exe, donde *n* es el número de compilación, en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Haga doble clic en SSMA para el paquete de extensiones de Sybase. *n*. Instale. exe.  
  
3.  En la página de bienvenida, haga clic en **Siguiente**.  
  
4.  En la página contrato de licencia para el usuario final, lea el contrato de licencia. Si está de acuerdo, active la casilla acepto **los términos del contrato de licencia** y, a continuación, haga clic en **siguiente**.  
  
5.  En la página elegir tipo de instalación, haga clic en **típica**.  
  
6.  En la página listo para instalar, haga clic en **instalar**.  
  
7.  En la página finalización del primer paso de la instalación, haga clic en **siguiente**.  
  
    Aparecerá un nuevo cuadro de diálogo en el que podrá seleccionar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a migrar las bases de datos de ase y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Las instancias con nombre van seguidas de una barra diagonal inversa y el nombre de la instancia.  
  
9. En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    La autenticación de Windows utilizará las credenciales de Windows para intentar iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la instancia de. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión y una contraseña.  
  
10. En la página Manage Server (administrar servidor), seleccione **install Utilities Database** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    Se crea la base de datos **sysdb** y se crean los procedimientos almacenados en esa base de datos.  
  
    Si la opción **instalar base de datos de prueba** está activada, se creará la base de datos del comprobador **ssmatesterdb_syb** .  
  
11. Para instalar las utilidades en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **volver a instancias**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **salir**.  
  
### <a name="sql-server-database-objects"></a>SQL Server objetos de base de datos  
Después de instalar el paquete de extensión, verá una tabla **ssma_syb. bcp_migration_packages** en la base de datos **sysdb** . También verá los siguientes procedimientos almacenados:  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
Cada vez que se migran datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Estos trabajos se denominan **ssma_syb paquete de migración de datos {GUID}** y se pueden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ver en el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nodo agente de en la carpeta trabajos.  
  
## <a name="sybase-providers"></a>Proveedores de Sybase  
Al migrar datos desde ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure, los datos se migran directamente entre ase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure. No pasa por SSMA, ya que esto ralentizaría la migración de datos.  
  
### <a name="installing-the-sybase-providers"></a>Instalación de los proveedores de Sybase  
Las instrucciones siguientes proporcionan los pasos de instalación básica para instalar proveedores de Sybase. Las instrucciones exactas variarán en función de la versión del programa de instalación de Sybase.  
  
> [!IMPORTANT]  
> Antes de ejecutar el programa de instalación, compruebe que no está infringiendo los contratos de licencia.  
  
1.  Ejecute el programa de instalación de Sybase ASE.  
  
2.  Seleccione instalación personalizada.  
  
3.  En la página selección de características, seleccione los proveedores de datos ODBC, OLE DB y ADO.NET.  
  
4.  Compruebe las características seleccionadas y, a continuación, haga clic en **Finalizar** para instalar el proveedor de datos.  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para el cliente de Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migración de bases de datos de Sybase ASE a SQL Server: Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
