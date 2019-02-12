---
title: Administrar usuarios de DQS en SSMS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d8d7e0c31b1e022445006598f791716d765b98c9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027986"
---
# <a name="manage-dqs-users-in-ssms"></a>Administrar usuarios de DQS en SSMS
  En este tema se describe cómo crear usuarios adicionales en la instancia de SQL Server con SQL Server Management Studio y cómo concederles roles de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) adecuados en la base de datos DQS_MAIN.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para crear el inicio de sesión de SQL y concederle los roles de DQS adecuados, debe usarse una cuenta de usuario de Windows que sea miembro del rol fijo de servidor adecuado (como securityadmin, serveradmin o sysadmin).  
  
##  <a name="GrantRoles"></a> Crear un inicio de sesión SQL y el rol de DQS de concesión  
  
1.  Inicie Microsoft SQL Server Management Studio.  
  
2.  En Microsoft SQL Server Management Studio, expanda la instancia de SQL Server y, a continuación, expanda **Seguridad**.  
  
3.  Haga clic con el botón derecho en la carpeta **Seguridad** , seleccione **Nuevo**y, después, haga clic en **Inicio de sesión**.  
  
4.  En el cuadro de diálogo **Inicio de sesión - Nuevo**, especifique el nombre de un usuario de Windows en el cuadro **Nombre de inicio de sesión**, especifique el tipo de autenticación como **Autenticación de Windows**y haga clic en **Buscar** para validar el usuario.  
  
    > [!NOTE]  
    >  DQS solo admite la autenticación de Windows; la autenticación de SQL Server no se admite.  
  
5.  Después de validar el usuario, haga clic en la página **Asignación de usuarios** en el panel izquierdo.  
  
6.  En el panel derecho, seleccione la casilla situada bajo la **mapa** columna para el **DQS_MAIN** de base de datos y, a continuación, seleccione el **dqs_administrator**, **dqs_kb_editor** , o **dqs_kb_operator** casilla de verificación en la **pertenencia al rol de la base de datos: DQS_MAIN** panel según el nivel de acceso necesario para el usuario.  
  
7.  En el cuadro de diálogo **Inicio de sesión - Nuevo**, haga clic en **Aceptar** para aplicar los cambios.  
  
    > [!NOTE]  
    >  Si concede el rol **dqs_administrator** a un usuario, aplica los cambios y, tras ello, vuelve a revisar los permisos de usuario, las otras dos casillas de roles de DQS (**dq_kb_editor** y **dqs_kb_operator**) también se activan.  
  
  
