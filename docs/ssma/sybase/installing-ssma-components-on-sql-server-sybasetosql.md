---
title: "Instalación de componentes SSMA en SQL Server (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 716a45f706292e3011ed5c8c2871bfc8176fb5a5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalación de componentes SSMA en SQL Server (SybaseToSQL)
Además de instalar SSMA, para usar la migración de datos del lado servidor, debe instalar también componentes en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de Sybase para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA para Sybase extensión Pack  
Las bases de datos, agrega el módulo de extensión SSMA **sysdb** y **ssmatesterdb_syb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. El **sysdb** base de datos contiene las tablas y procedimientos almacenados necesarios para migrar los datos. El **ssmatester_syb** base de datos contiene el esquema **ssma_sybase_utilities**, en la que se crean los objetos (tablas, desencadenadores, vistas) utilizados por el componente de la herramienta de comprobación SSMA.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabajos del agente cuando se usa el motor de migración de datos de lado de servidor para migrar los datos.  
  
### <a name="installing-the-extension-pack"></a>Instalar el módulo de extensión  
Puede instalar el paquete de extensión cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro del rol de servidor sysadmin en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar el módulo de extensión**  
  
1.  Copie SSMA para Sybase extensión Pack. *n*. Install.exe, donde  *n*  es el número de compilación, en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Haga doble clic en SSMA para Sybase extensión Pack. *n*. Install.exe.  
  
3.  En la página de bienvenida, haga clic en **siguiente**.  
  
4.  En la página Contrato de licencia de usuario final, lea el contrato de licencia. Si los acepta, seleccione la **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
5.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
6.  En la página Listo para instalar, haga clic en **instalar**.  
  
7.  En la página de primer paso de instalación de completado, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo nuevo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde se pueden migrar bases de datos de ASE y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se realizarán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
9. En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, debe escribir una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nombre de inicio de sesión y una contraseña.  
  
10. En la página Administrar el servidor, seleccione **instalar bases de datos de utilidades**  *n* , donde  *n*  es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** se crea la base de datos y los procedimientos almacenados se crean en esa base de datos.  
  
    Si **instalar bases de datos de evaluador** está activada la opción de la herramienta de comprobación **ssmatesterdb_syb** se creará la base de datos.  
  
11. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], seleccione **volver a instancias**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **salir**.  
  
### <a name="sql-server-database-objects"></a>Objetos de base de datos SQL Server  
Después de instalar el paquete de extensión, tendrá que vea una **ssma_syb.bcp_migration_packages** tabla el **sysdb** base de datos. También verá los siguientes procedimientos almacenados:  
  
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
  
Cada vez que se van a migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabajo del agente. Estos trabajos se denominan **{GUID} del paquete de migración de datos de ssma_syb**y pueden verse en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nodo de agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] en la carpeta de trabajos.  
  
## <a name="sybase-providers"></a>Proveedores de Sybase  
Al migrar datos desde ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure, la migración de datos directamente entre ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure. No se pasa a través de SSMA porque esto podría ralentizar la migración de datos.  
  
### <a name="installing-the-sybase-providers"></a>Instalar a los proveedores de Sybase  
Las siguientes instrucciones proporcionan los pasos de instalación básico para la instalación de proveedores de Sybase. Las instrucciones exactas variarán según la versión del programa de instalación de Sybase.  
  
> [!IMPORTANT]  
> Antes de ejecutar el programa de instalación, compruebe que no están infringiendo los contratos de licencia.  
  
1.  Ejecute el programa de instalación de Sybase ASE.  
  
2.  Seleccione el programa de instalación personalizado.  
  
3.  En la página de selección de características, seleccione los proveedores de datos ODBC, OLE DB y ADO.NET.  
  
4.  Comprobar las características seleccionadas y, a continuación, haga clic en **finalizar** para instalar el proveedor de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase cliente &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

