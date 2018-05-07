---
title: Instalación de componentes SSMA en SQL Server (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: d75694edf4af06ec2d1e442ecebacaf971ba86de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalación de componentes SSMA en SQL Server (OracleToSQL)
Además de instalar SSMA, debe instalar también componentes en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de Oracle para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA para paquete de extensión de Oracle  
Las bases de datos, agrega el módulo de extensión SSMA **sysdb** y **ssmatesterdb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La base de datos **sysdb** contiene las tablas y procedimientos almacenados necesarios para migrar los datos y las funciones definidas por el usuario que emulan las funciones del sistema de Oracle. El **ssmatesterdb** base de datos contiene las tablas y procedimientos que son necesarios para el componente de evaluador.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabajos del agente cuando se usa el motor de migración de datos de lado de servidor para migrar los datos.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de instalar SSMA para componentes de servidor de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], asegúrese de que el sistema cumple los requisitos siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está instalada la instancia. SSMA no es compatible con SQL Server 2008 Express Edition.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El proveedor de cliente de Oracle o el proveedor OLE DB para Oracle y la conectividad a la base de datos de Oracle que se va a migrar. Puede instalar a proveedores desde el CD del producto de Oracle o el sitio Web de Oracle.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio de explorador debe estar ejecutándose durante la instalación. Se utiliza para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el Asistente para la instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser se está ejecutando, pero aún no ve una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar Firewall de Windows para desbloquear temporalmente el puerto, o puede deshabilitar temporalmente el Firewall de Windows. También tendrá que deshabilitar temporalmente el software antivirus. Asegúrese de que habilita los servidores de seguridad y el software antivirus tras la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalar el módulo de extensión  
Puede instalar el paquete de extensión cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro de la **sysadmin** rol de servidor en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar el módulo de extensión**  
  
1.  Si aún no lo ha hecho, extraiga todos los archivos del archivo Zip de SSMA.  
  
    Según la versión de WinZip tiene, puede haga doble clic en el archivo, o haga clic en el archivo y seleccione **extraer todo** o **abierto en WinZip**. Siga las instrucciones en la interfaz de usuario de WinZip para extraer los archivos.  
  
2.  Copie SSMA para paquete de extensión de Oracle. *n*. Install.exe, donde *n* es el número de compilación, en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
3.  Haga doble clic en SSMA para paquete de extensión de Oracle. *n*. Install.exe.  
  
4.  En la página de bienvenida, haga clic en **siguiente**.  
  
5.  En la página Contrato de licencia de usuario final, lea el contrato de licencia. Si los acepta, seleccione la **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
6.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
7.  En la página Listo para instalar, haga clic en **instalar**.  
  
8.  En la página de primer paso de instalación de completado, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo nuevo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para la instalación del paquete de extensión.  
  
9. Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde se pueden migrar esquemas de Oracle y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se realizarán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
10. En la página de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, debe escribir una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nombre de inicio de sesión y una contraseña.  
  
11. En la página siguiente, seleccione **instalar bases de datos de utilidades** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** se crea la base de datos y las funciones definidas por el usuario y procedimientos almacenados se crean en esa base de datos.  
  
    Si **instalar bases de datos de evaluador** está activada la opción de la herramienta de comprobación **ssmatesterdb** se creará la base de datos.  
  
12. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], seleccione **Sí**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **No**.  
  
13. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o mediante la utilidad sqlcmd, ejecute el siguiente script para habilitar CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Si CLR no está habilitado, recibirá el siguiente error cuando se conecta SSMA a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    SSMA no pudo recuperar la información de versión del ensamblado de módulo de extensión. Vuelva a instalar el paquete de extensión en el servidor de base de datos.  
  
### <a name="sql-server-database-objects"></a>Objetos de base de datos SQL Server  
Después de instalar el paquete de extensión, tendrá que vea una **ssma_oracle.bcp_migration_packages** tabla, un **ssma_oracle.db_storage** tabla y un **ssma_oracle.db_error_list** tabla el **sysdb** base de datos. También verá muchos procedimientos almacenados y funciones definidas por el usuario en el **ssma_oracle** esquema.  
  
Cada vez que se van a migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabajo del agente. Estos trabajos se denominan **{GUID} del paquete de migración de datos de ssma_oracle**y pueden verse en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nodo de agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] en la carpeta de trabajos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para cliente de Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
