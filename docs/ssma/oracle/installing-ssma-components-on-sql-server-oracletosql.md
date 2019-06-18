---
title: Instalación de componentes de SSMA en SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2041901a851ca755b1079535ccbf763472ec7bc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055675"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalación de componentes de SSMA en SQL Server (OracleToSQL)
Además de instalar SSMA, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de Oracle para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA para Oracle: paquete de extensión  
Las bases de datos, agrega el paquete de extensiones SSMA **sysdb** y **ssmatesterdb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La base de datos **sysdb** contiene las tablas y procedimientos almacenados que son necesarios para migrar datos y las funciones definidas por el usuario que emulan las funciones del sistema de Oracle. El **ssmatesterdb** base de datos contiene las tablas y procedimientos necesarios para el componente herramienta de comprobación.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los trabajos del agente cuando se usa el motor de migración de datos de lado servidor para migrar los datos.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de instalar SSMA para los componentes de servidor de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que el sistema cumple los requisitos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala la instancia. SSMA no es compatible con SQL Server 2008 Express Edition.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El proveedor de cliente de Oracle o el proveedor OLE DB para Oracle y la conectividad a la base de datos de Oracle que se va a migrar. Puede instalar a proveedores desde el CD del producto de Oracle o el sitio Web de Oracle.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser debe estar ejecutándose durante la instalación. Esto se usa para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Asistente para instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser se está ejecutando, pero no vea una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar Firewall de Windows para desbloquear temporalmente el puerto, o puede deshabilitar temporalmente el Firewall de Windows. También es posible que deba deshabilitar temporalmente el software antivirus. Asegúrese de habilitar los servidores de seguridad y el software antivirus tras la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalar el paquete de extensiones  
Puede instalar el paquete de extensiones de cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar el módulo de extensión, debe ser miembro de la **sysadmin** rol de servidor en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar el paquete de extensiones**  
  
1.  Si aún no lo ha hecho, extraiga todos los archivos del archivo Zip de SSMA.  
  
    Según la versión de WinZip tiene, puede haga doble clic en el archivo, o haga clic en el archivo y seleccione **extraer todo** o **abierto en WinZip**. Siga las instrucciones de la interfaz de usuario de WinZip para extraer los archivos.  
  
2.  Copie SSMA para Oracle: paquete de extensión. *n*. Install.exe, donde *n* es el número de compilación, en el equipo que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Haga doble clic en SSMA para Oracle: paquete de extensión. *n*. Install.exe.  
  
4.  En la página de bienvenida, haga clic en **siguiente**.  
  
5.  En la página Contrato de licencia de usuario final, lea el contrato de licencia. Si está de acuerdo, seleccione el **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
6.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
7.  En la página Listo para instalar, haga clic en **instalar**.  
  
8.  En el completado de la página del primer paso de instalación, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
9. Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a migrar esquemas de Oracle y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se seguirán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
10. En la página de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y la contraseña.  
  
11. En la siguiente página, seleccione **instalar base de datos de utilidades** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** se crea la base de datos y las funciones definidas por el usuario y procedimientos almacenados se crean en esa base de datos.  
  
    Si **instalar base de datos de evaluador** está activada la opción de la herramienta de comprobación **ssmatesterdb** se creará la base de datos.  
  
12. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **Sí**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **No**.  
  
13. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o mediante la utilidad sqlcmd, ejecute el siguiente script para habilitar CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Si CLR no está habilitado, recibirá el siguiente error cuando se conecta SSMA a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    SSMA no pudo recuperar la información de versión del ensamblado de módulo de extensión. Vuelva a instalar el paquete de extensiones en el servidor de base de datos.  
  
### <a name="sql-server-database-objects"></a>Objetos de base de datos SQL Server  
Después de instalar el paquete de extensiones, tendrá un vea un **ssma_oracle.bcp_migration_packages** tabla, un **ssma_oracle.db_storage** tabla y un **ssma_oracle.db_error_list** de tabla en la **sysdb** base de datos. También verá muchos de los procedimientos almacenados y funciones definidas por el usuario en el **ssma_oracle** esquema.  
  
Cada vez que migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Estos trabajos se denominan **{GUID} del paquete de migración de datos de ssma_oracle**y son visibles en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo de agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en la carpeta Jobs.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
