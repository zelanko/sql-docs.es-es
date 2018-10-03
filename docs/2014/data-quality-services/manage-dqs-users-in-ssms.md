---
title: Administrar usuarios de DQS en SSMS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b269ec84e2aa2227cc8edf8a0808fc7df0dce31
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077482"
---
# <a name="manage-dqs-users-in-ssms"></a>Administrar usuarios de DQS en SSMS
  En este tema se describe cómo crear usuarios adicionales en la instancia de SQL Server con SQL Server Management Studio y cómo concederles roles de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) adecuados en la base de datos DQS_MAIN.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para crear el inicio de sesión de SQL y concederle los roles de DQS adecuados, debe usarse una cuenta de usuario de Windows que sea miembro del rol fijo de servidor adecuado (como securityadmin, serveradmin o sysadmin).  
  
##  <a name="GrantRoles"></a> Crear un inicio de sesión SQL y el rol de DQS de concesión  
  
1.  Inicie Microsoft SQL Server Management Studio.  
  
2.  En Microsoft SQL Server Management Studio, expanda la instancia de SQL Server y, a continuación, expanda **Seguridad**.  
  
3.  Haga clic con el botón secundario en la carpeta **Seguridad** , seleccione **Nuevo**y, a continuación, haga clic en **Inicio de sesión**.  
  
4.  En el cuadro de diálogo **Inicio de sesión - Nuevo** , especifique el nombre de un usuario de Windows en el cuadro **Nombre de inicio de sesión** , especifique el tipo de autenticación como **Autenticación de Windows**y haga clic en **Buscar** para validar el usuario.  
  
    > [!NOTE]  
    >  DQS solo admite la autenticación de Windows; la autenticación de SQL Server no se admite.  
  
5.  Después de validar el usuario, haga clic en la página **Asignación de usuarios** en el panel izquierdo.  
  
6.  En el panel derecho, active la casilla en la columna **Asignar** para la base de datos **DQS_MAIN** y, a continuación, active la casilla **dqs_administrator**, **dqs_kb_editor**o **dqs_kb_operator** en el panel **Pertenencia al rol de la base de datos para: DQS_MAIN** , dependiendo del nivel de acceso necesario para el usuario.  
  
7.  En el cuadro de diálogo **Inicio de sesión – Nuevo** , haga clic en **Aceptar** para aplicar los cambios.  
  
    > [!NOTE]  
    >  Si concede el rol **dqs_administrator** a un usuario, aplica los cambios y, a continuación, vuelve a revisar los permisos de usuario, las otras dos casillas de roles de DQS (**dq_kb_editor** y **dqs_kb_operator**) también se activan.  
  
  
