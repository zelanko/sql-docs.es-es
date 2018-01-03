---
title: Crear un administrador de dominio de puntos de acceso (AP)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed52bf78-2b0a-4252-98a7-8c2805e22d3d
caps.latest.revision: "7"
ms.openlocfilehash: 0ebc616d28fe734b9dac52303641390ce9bc0957
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="create-an-aps-domain-administrator"></a>Crear un administrador de dominio APS
Algunas operaciones requieren privilegios de administrador de dominio de sistema de la plataforma de análisis. Explica cómo crear administradores de dominio de aplicación adicionales.  
  
## <a name="create-a-domain-administrator"></a>Crear un administrador de dominio  
Tener permisos suficientes para configurar todos los nodos APS, el usuario que ejecuta el **APS Configuration Manager** (`dwconfig.exe`) debe ser un miembro de la **Admins. del dominio** grupo. Para iniciar y detener los servicios de puntos de acceso, el usuario debe ser miembro de la **PdwControlNodeAccess** grupo.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para agregar un usuario al grupo Admins. del dominio  
  
1.  Inicie sesión en el nodo activo de AD  **(*appliance_domain*-AD01 ** o  ***appliance_domain*-AD02**) usa un dominio de aplicación existente cuenta de administrador.  
  
2.  En el menú Iniciar, haga clic en **Ejecutar**. En el **abiertos** , escriba **dsa.msc**. Haga clic en **Aceptar**.  
  
3.  En el **equipos y usuarios de Active Directory** de programa, haga clic en **usuarios**, seleccione **New**y, a continuación, haga clic en **usuario**.  
  
4.  En el **nuevo objeto: usuario** cuadro de diálogo, complete la descripción del nuevo usuario y, a continuación, haga clic en **siguiente**.  
  
    Complete el cuadro de diálogo de contraseña y, a continuación, haga clic en **siguiente**.  
  
    > [!WARNING]  
    > PDW de SQL Server no admite el carácter de signo de dólar ($) en el Administrador de dominio o las contraseñas de administrador local. Una contraseña que contenga un signo de dólar, será válida y puede usar pero puede bloquear las actividades de actualización y mantenimiento  
  
    Confirme la nueva descripción del usuario y, a continuación, haga clic en **finalizar**.  
  
5.  En la lista de usuarios, haga doble clic en el nuevo usuario para abrir el cuadro de diálogo de propiedades de usuario.  
  
6.  En el **miembro de** , haga clic en **agregar**.  
  
    Tipo **Admins. del dominio; PdwControlNodeAccess** y, a continuación, haga clic en **comprobar nombres**. Haga clic en **Aceptar**.  
  
    Esto agrega el nuevo usuario a la **Admins. del dominio** grupo y la **PdwControlNodeAccess** grupo. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41;](launch-the-configuration-manager.md)  
  
