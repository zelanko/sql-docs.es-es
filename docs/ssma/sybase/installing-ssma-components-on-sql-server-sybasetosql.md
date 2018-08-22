---
title: Instalación de componentes de SSMA en SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c6090d5e24f7ba6fe6c06546f5f432a3c8eaa4ab
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393253"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalación de componentes de SSMA en SQL Server (SybaseToSQL)
Además de instalar SSMA para usar la migración de datos del lado servidor, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de Sybase para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA para Sybase extensión Pack  
Las bases de datos, agrega el paquete de extensiones SSMA **sysdb** y **ssmatesterdb_syb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El **sysdb** base de datos contiene las tablas y procedimientos almacenados que son necesarios para migrar los datos. El **ssmatester_syb** base de datos contiene el esquema **ssma_sybase_utilities**, en la que se crean los objetos (tablas, desencadenadores, vistas) utilizados por el componente de evaluador SSMA.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los trabajos del agente cuando se usa el motor de migración de datos de lado servidor para migrar los datos.  
  
### <a name="installing-the-extension-pack"></a>Instalar el paquete de extensiones  
Puede instalar el paquete de extensiones de cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar el módulo de extensión, debe ser miembro del rol de servidor sysadmin en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar el paquete de extensiones**  
  
1.  Copie SSMA para Sybase extensión Pack. *n*. Install.exe, donde *n* es el número de compilación, en el equipo que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Haga doble clic en SSMA para Sybase extensión Pack. *n*. Install.exe.  
  
3.  En la página de bienvenida, haga clic en **siguiente**.  
  
4.  En la página Contrato de licencia de usuario final, lea el contrato de licencia. Si está de acuerdo, seleccione el **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
5.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
6.  En la página Listo para instalar, haga clic en **instalar**.  
  
7.  En el completado de la página del primer paso de instalación, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a migrar bases de datos de ASE y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se seguirán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
9. En la página parámetros de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y la contraseña.  
  
10. En la página Administrar servidor, seleccione **instalar base de datos de utilidades** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** se crea la base de datos y los procedimientos almacenados se crean en esa base de datos.  
  
    Si **instalar base de datos de evaluador** está activada la opción de la herramienta de comprobación **ssmatesterdb_syb** se creará la base de datos.  
  
11. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **volver a instancias**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **salir**.  
  
### <a name="sql-server-database-objects"></a>Objetos de base de datos SQL Server  
Después de instalar el paquete de extensiones, tendrá un vea un **ssma_syb.bcp_migration_packages** de tabla en la **sysdb** base de datos. También verá los siguientes procedimientos almacenados:  
  
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
  
Cada vez que migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Estos trabajos se denominan **{GUID} del paquete de migración de datos de ssma_syb**y son visibles en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo de agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en la carpeta Jobs.  
  
## <a name="sybase-providers"></a>Proveedores de Sybase  
Al migrar datos desde el ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure, la migración de datos directamente entre el ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure. No se pasa a través de SSMA porque esto podría ralentizar la migración de datos.  
  
### <a name="installing-the-sybase-providers"></a>Instalar a los proveedores de Sybase  
Las instrucciones siguientes proporcionan los pasos de instalación básica para instalar proveedores de Sybase. Las instrucciones exactas variarán dependiendo de la versión del programa de instalación de Sybase.  
  
> [!IMPORTANT]  
> Antes de ejecutar el programa de instalación, compruebe que no están infringiendo los contratos de licencia.  
  
1.  Ejecute el programa de instalación de Sybase ASE.  
  
2.  Seleccione instalación personalizada.  
  
3.  En la página Selección de características, seleccione los proveedores de datos ODBC, OLE DB y ADO.NET.  
  
4.  Compruebe las características seleccionadas y, a continuación, haga clic en **finalizar** para instalar el proveedor de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
