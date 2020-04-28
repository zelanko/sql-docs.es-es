---
title: Instalación de componentes de SSMA en SQL Server (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 64040f4a0caf8253e6d6e8a3b00ff21e0cebe6d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68075347"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalación de componentes de SSMA en SQL Server (MySQLToSql)
Además de instalar SSMA, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes incluyen el paquete de extensión SSMA, que admite la migración de datos y los proveedores de MySQL para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA para el paquete de extensiones de MySQL  
El paquete de extensión SSMA agrega una base de datos, **sysdb**, a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instancia especificada de. Esta base de datos contiene las tablas y los procedimientos almacenados necesarios para migrar los datos.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente, cuando el motor de migración de datos del lado servidor se usa para migrar los datos.  
  
### <a name="prerequisites"></a>Prerrequisitos  
Antes de instalar los componentes de SSMA para MySQL Server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
-   El proveedor de cliente de MySQL y la conectividad a la base de datos MySQL que desea migrar. Puede instalar proveedores en el sitio web de MySQL o en el soporte del producto de MySQL.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser debe estar en ejecución durante la instalación. Se utiliza para rellenar una lista de las instancias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de en el Asistente para la instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio explorador de se está ejecutando, pero todavía no ve una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar el Firewall de Windows para desbloquear temporalmente el puerto o puede deshabilitar temporalmente el Firewall de Windows. Es posible que también tenga que deshabilitar temporalmente el software antivirus. Asegúrese de habilitar los firewalls y el software antivirus después de la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalación del paquete de extensión  
Puede instalar el paquete de extensión en cualquier momento antes de migrar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos a.  
  
> [!IMPORTANT]  
> Para instalar el paquete de extensión, debe ser miembro del rol de servidor **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar el paquete de extensión**  
  
1.  Copie SSMA para el paquete de extensiones de MySQL. *n*. Instale. exe, donde *n* es el número de compilación, en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Haga doble clic en SSMA para el paquete de extensiones de MySQL. *n*. Instale. exe.  
  
3.  En el cuadro de diálogo de bienvenida, haga clic en **siguiente**.  
  
4.  En el cuadro de diálogo contrato de licencia para el usuario final, lea el contrato de licencia. Si está de acuerdo, active la casilla acepto **los términos del contrato de licencia** y, a continuación, haga clic en **siguiente**.  
  
5.  En el cuadro de diálogo elegir tipo de instalación, haga clic en **típica**.  
  
6.  En el cuadro de diálogo listo para instalar, haga clic en **instalar**.  
  
7.  En el cuadro de diálogo finalización del primer paso de la instalación, haga clic en **siguiente**.  
  
    Aparecerá un nuevo cuadro de diálogo en el que podrá seleccionar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a migrar los esquemas de MySQL y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Las instancias con nombre van seguidas de una barra diagonal inversa y el nombre de la instancia.  
  
9. En el cuadro de diálogo conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    La autenticación de Windows utilizará las credenciales de Windows para intentar iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la instancia de. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión y una contraseña.  
  
10. En el siguiente cuadro de diálogo, seleccione **install Utilities Database** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    La base de datos **sysdb** se crea con las tablas y los procedimientos almacenados necesarios para la migración de datos (mediante el motor de migración de datos del lado servidor) se crean en esa base de datos.  
  
11. Para instalar las utilidades en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **sí**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **no**.  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para MySQL Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migración de bases de datos de MySQL a SQL Server: Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
