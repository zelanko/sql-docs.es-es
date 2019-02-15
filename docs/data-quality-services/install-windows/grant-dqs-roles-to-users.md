---
title: Conceder roles de DQS a los usuarios | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 00246af5bd0b577d7f1c7aebf4711d58a9828865
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028446"
---
# <a name="grant-dqs-roles-to-users"></a>Conceder roles de DQS a los usuarios

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear los inicios de sesión de SQL según una entidad de seguridad de Windows y cómo conceder roles de [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) en la base de datos DQS_MAIN.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Debe haber completado la instalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ejecutando el archivo DQSInstaller.exe. Para obtener más información, vea [Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor adecuado (como securityadmin, serveradmin o sysadmin) para crear el inicio de sesión de SQL y concederle los roles de DQS.  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>Para crear un inicio de sesión de SQL y conceder los roles de DQS  
  
1.  Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda la instancia de SQL Server y, a continuación expanda **Seguridad**.  
  
3.  Haga clic con el botón derecho en la carpeta **Seguridad** , seleccione **Nuevo**y, después, haga clic en **Inicio de sesión**.  
  
4.  En el cuadro de diálogo **Inicio de sesión - Nuevo**, especifique el nombre de un usuario de Windows en el cuadro **Nombre de inicio de sesión**, especifique el tipo de autenticación como **Autenticación de Windows**y haga clic en **Buscar** para validar el usuario.  
  
5.  Después de validar el usuario, haga clic en la página **Asignación de usuarios** en el panel izquierdo.  
  
6.  En el panel derecho, active la casilla de la columna **Asignar** para la base de datos **DQS_MAIN** y, después, active la casilla **dqs_administrator**, **dqs_kb_editor** o **dqs_kb_operator** en el panel  **Pertenencia al rol de la base de datos para: DQS_MAIN**, según el nivel de acceso necesario para el usuario. Para obtener más información acerca de los tres roles de DQS, vea [Seguridad DQS](../../data-quality-services/dqs-security.md).  
  
7.  En el cuadro de diálogo **Inicio de sesión - Nuevo**, haga clic en **Aceptar** para aplicar los cambios.  
  
    > [!NOTE]  
    >  Si concede el rol **dqs_administrator** a un usuario, aplica los cambios y, tras ello, vuelve a revisar los permisos de usuario, las otras dos casillas de roles de DQS (**dq_kb_editor** y **dqs_kb_operator**) también se activan.  
  
## <a name="next-steps"></a>Next Steps  
 Intente iniciar sesión en el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] con la cuenta de usuario de Windows para la que ha creado un inicio de sesión de SQL y a la que ha concedido un rol de DQS.  
  
## <a name="see-also"></a>Consulte también  
 [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
