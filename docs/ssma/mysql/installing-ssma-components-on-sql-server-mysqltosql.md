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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075347"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalación de componentes de SSMA en SQL Server (MySQLToSql)
Además de instalar SSMA, también debe instalar los componentes en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes incluyen el módulo de extensión SSMA, que admite la migración de datos y proveedores de MySQL para habilitar la conectividad de servidor a servidor.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA para el paquete de extensión de MySQL  
Una base de datos, agrega el paquete de extensiones SSMA **sysdb**, a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta base de datos contiene las tablas y procedimientos almacenados que son necesarios para migrar los datos.  
  
Además, al migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente, cuando se usa el motor de migración de datos de lado servidor para migrar los datos.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de instalar SSMA para los componentes de servidor de MySQL en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El proveedor de cliente de MySQL y la conectividad a la base de datos MySQL que se va a migrar. Puede instalar a proveedores desde el CD del producto de MySQL o sitio MySQL Web.  
  
-   El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser debe estar ejecutándose durante la instalación. Esto se usa para rellenar una lista de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Asistente para instalación. Puede deshabilitar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser después de la instalación.  
  
    > [!NOTE]  
    > Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio Browser se está ejecutando, pero no vea una lista de instancias en el programa de instalación, debe desbloquear el puerto UDP 1434. Puede usar Firewall de Windows para desbloquear temporalmente el puerto, o puede deshabilitar temporalmente el Firewall de Windows. También es posible que deba deshabilitar temporalmente el software antivirus. Asegúrese de habilitar los servidores de seguridad y el software antivirus tras la instalación.  
  
### <a name="installing-the-extension-pack"></a>Instalar el paquete de extensiones  
Puede instalar el paquete de extensiones de cualquier momento antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar el módulo de extensión, debe ser miembro de la **sysadmin** rol de servidor en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar el paquete de extensiones**  
  
1.  Copie SSMA para el paquete de extensión de MySQL. *n*. Install.exe, donde *n* es el número de compilación, en el equipo que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Haga doble clic en SSMA para el paquete de extensión de MySQL. *n*. Install.exe.  
  
3.  En el cuadro de diálogo de bienvenida, haga clic en **siguiente**.  
  
4.  En el cuadro de diálogo Contrato de licencia de usuario final, lea el contrato de licencia. Si está de acuerdo, seleccione el **acepto los términos del contrato de licencia** casilla de verificación y, a continuación, haga clic en **siguiente**.  
  
5.  En el cuadro de diálogo Elegir tipo de instalación, haga clic en **típica**.  
  
6.  En Listo al cuadro de diálogo de instalación, haga clic en **instalar**.  
  
7.  En la el cuadro de diálogo del primer paso de instalación completado, haga clic en **siguiente**.  
  
    Aparecerá un cuadro de diálogo, en el que se seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación del paquete de extensión.  
  
8.  Seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a migrar esquemas de MySQL y, a continuación, haga clic en **siguiente**.  
  
    La instancia predeterminada tiene el mismo nombre que el equipo. Se seguirán las instancias con nombre por una barra diagonal inversa y el nombre de instancia.  
  
9. En el cuadro de diálogo de conexión, seleccione el método de autenticación y, a continuación, haga clic en **siguiente**.  
  
    Autenticación de Windows usará las credenciales de Windows para intentar iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si selecciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, debe escribir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de inicio de sesión y la contraseña.  
  
10. En el siguiente cuadro de diálogo, seleccione **instalar base de datos de utilidades** *n*, donde *n* es el número de versión y, a continuación, haga clic en **siguiente**.  
  
    El **sysdb** base de datos se crea con las tablas y procedimientos almacenados necesarios para la migración de datos (mediante el motor de migración de datos de lado servidor) se crean en esa base de datos.  
  
11. Para instalar las utilidades a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **Sí**y, a continuación, haga clic en **siguiente**. O bien, para salir del asistente, haga clic en **No**.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para MySQL cliente &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
