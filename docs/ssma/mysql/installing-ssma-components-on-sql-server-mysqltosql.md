---
title: "Instalación de componentes SSMA en SQL Server (MySQLToSql) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9544fb62402871b9a93284df88e0082f62fec582
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalación de componentes SSMA en SQL Server (MySQLToSql)
Además de instalar SSMA, debe instalar también componentes en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de MySQL para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA para paquete de extensión de MySQL  
El módulo de extensión SSMA agrega una base de datos, **sysdb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esta base de datos contiene las tablas y procedimientos almacenados necesarios para migrar los datos.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabajos del agente, al motor de migración de datos de lado de servidor se usa para migrar los datos.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de instalar SSMA para componentes de servidor de MySQL en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 o una versión posterior.  
  
-   El proveedor de cliente de MySQL y la conectividad a la base de datos de MySQL que se va a migrar. Puede instalar a proveedores desde el CD del producto de MySQL o el sitio MySQL Web.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio de explorador debe estar ejecutándose durante la instalación. Se utiliza para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el Asistente para la instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] servicio Browser se está ejecutando, pero aún no ve una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar Firewall de Windows para desbloquear temporalmente el puerto, o puede deshabilitar temporalmente el Firewall de Windows. También tendrá que deshabilitar temporalmente el software antivirus. Asegúrese de que habilita los servidores de seguridad y el software antivirus tras la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalar el módulo de extensión  
Puede instalar el paquete de extensión cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro de la **sysadmin** rol de servidor en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar el módulo de extensión**  
  
1.  Copie SSMA para paquete de extensión de MySQL. *n*. Install.exe, donde  *n*  es el número de compilación, en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Haga doble clic en SSMA para paquete de extensión de MySQL. *n*. Install.exe.  
  
3.  En el cuadro de diálogo de bienvenida, haga clic en **siguiente**.  
  
4.  En el cuadro de diálogo del contrato de licencia de usuario final, lea el contrato de licencia. Si los acepta, seleccione la **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
5.  En el cuadro de diálogo Elegir tipo de instalación, haga clic en **típica**.  
  
6.  En la lista al cuadro de diálogo de instalación, haga clic en **instalar**.  
  
7.  En el cuadro de diálogo del primer paso de instalación de completado, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo nuevo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde se pueden migrar esquemas de MySQL y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se realizarán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
9. En el cuadro de diálogo de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, debe escribir una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nombre de inicio de sesión y una contraseña.  
  
10. En el siguiente cuadro de diálogo, seleccione **instalar bases de datos de utilidades**  *n* , donde  *n*  es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** base de datos se crea con las tablas y procedimientos almacenados necesarios para la migración de datos (mediante el motor de migración de datos de lado de servidor) se crean en esa base de datos.  
  
11. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], seleccione **Sí**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **No**.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para cliente de MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

