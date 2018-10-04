---
title: Configurar permisos del sistema de archivos para el acceso al motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 137f2f2e02e7e1dd91e93a246401108c68d00a11
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074405"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>Configurar permisos del sistema de archivos para el acceso al motor de base de datos
  En este tema se describe cómo conceder a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]acceso al sistema de archivos de la ubicación donde se almacenan los archivos de base de datos. El servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe tener permiso del sistema de archivos de Windows para obtener acceso a la carpeta de archivos donde se almacenan los archivos de base de datos. El permiso para tener acceso a la ubicación predeterminada se configura durante la instalación. Si coloca los archivos de base de datos en una ubicación diferente, es posible que tenga que seguir estos pasos para conceder a [!INCLUDE[ssDE](../../includes/ssde-md.md)] permisos de control total a dicha ubicación.  
  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , se asignan permisos al SID por servicio para cada uno de sus servicios. Este sistema ayuda a conseguir el aislamiento del servicio y una defensa optimizada. El SID por servicio se deriva del nombre del servicio y es único para cada servicio. El tema [Configurar los permisos y las cuentas de servicio de Windows](configure-windows-service-accounts-and-permissions.md) describe el SID por servicio y proporciona los nombres en la sección **Derechos y privilegios de Windows**. El permiso de acceso en la ubicación de los archivos se debe asignar al SID por servicio.  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>Para conceder permisos del sistema de archivos al SID por servicio  
  
1.  Utilice el Explorador de Windows para navegar a la ubicación del sistema de archivos donde se almacenan los archivos de base de datos. Haga clic con el botón derecho en la carpeta del sistema de archivos y, después, haga clic en **Propiedades**.  
  
2.  Haga clic en la pestaña **Seguridad** , haga clic en **Editar**y, a continuación, en **Agregar**.  
  
3.  En el cuadro de diálogo **Seleccionar usuarios, equipos, cuentas de servicio o grupos** , haga clic en **Ubicaciones**, seleccione el nombre del equipo en la parte superior de la lista de ubicaciones y, a continuación, haga clic en **Aceptar**.  
  
4.  En el **escriba los nombres de objeto para seleccionar** , escriba el nombre del SID por servicio aparece en el tema de libros en pantalla de **Configure Windows Service Accounts and Permissions**. (Para el [!INCLUDE[ssDE](../../includes/ssde-md.md)] SID por servicio, utilice **NT SERVICE\MSSQLSERVER** para una instancia predeterminada, o **NT SERVICE\MSSQL$ InstanceName** para una instancia con nombre.)  
  
5.  Para validar la entrada, haga clic en **Comprobar nombres** . A menudo, se produce un error en la validación, y es posible que aparezca un mensaje indicando que no se encontró el nombre. Al hacer clic en **Aceptar**, aparece un cuadro de diálogo **Se encontraron varios nombres** .  
  
6.  Ahora seleccione el SID por servicio, bien **MSSQLSERVER** o **NT SERVICE\MSSQL$ InstanceName**y, a continuación, haga clic en **Aceptar**.  
  
7.  Haga clic en **Aceptar** de nuevo para regresar al cuadro de diálogo **Permisos** .  
  
8.  En el **grupo o usuario** nombres, seleccione el SID por servicio y, a continuación, en el **permisos para** \<nombre > cuadro, seleccione el **permitir** casilla de verificación para  **Control total**.  
  
9. Haga clic en **Aplicar**y, a continuación, haga clic dos veces en **Aceptar** para salir.  
  
## <a name="see-also"></a>Vea también  
 [Administrar el servicio del motor de base de datos](manage-the-database-engine-services.md)   
 [Mover bases de datos del sistema](../../relational-databases/databases/system-databases.md)   
 [Mover bases de datos de usuario](../../relational-databases/databases/move-user-databases.md)  
  
  
