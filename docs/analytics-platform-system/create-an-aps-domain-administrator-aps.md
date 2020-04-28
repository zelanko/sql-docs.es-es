---
title: Crear un administrador de dominio
description: Algunas operaciones requieren privilegios de administrador de dominio de Analytics Platform System. En este artículo se explica cómo crear administradores de dominio de aplicación adicionales.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401230"
---
# <a name="create-an-aps-domain-administrator"></a>Creación de un administrador de dominio APS
Algunas operaciones requieren privilegios de administrador de dominio de Analytics Platform System. En este artículo se explica cómo crear administradores de dominio de aplicación adicionales.  
  
## <a name="create-a-domain-administrator"></a>Crear un administrador de dominio  
Para tener permisos suficientes para configurar todos los nodos APS, el usuario que ejecuta el **APS Configuration Manager** (`dwconfig.exe`) debe ser miembro del grupo **Admins** . del dominio. Para iniciar y detener los servicios APS, el usuario debe ser miembro del grupo **PdwControlNodeAccess** .  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para agregar un usuario al grupo Admins. del dominio  
  
1.  Inicie sesión en el nodo Active **Directory _(\_dominio de aplicación_-AD01** o ** _\_equipo dominio_-AD02**) mediante una cuenta de administrador de dominio de dispositivo existente.  
  
2.  En el menú Inicio, haga clic en **Ejecutar**. En el cuadro **abrir** , escriba **DSA. msc**. Haga clic en **OK**.  
  
3.  En el programa **usuarios y equipos de Active Directory** , haga clic con el botón secundario en **usuarios**, seleccione **nuevo**y, a continuación, haga clic en **usuario**.  
  
4.  En el cuadro de diálogo **nuevo objeto-usuario** , complete la descripción del nuevo usuario y, a continuación, haga clic en **siguiente**.  
  
    Complete el cuadro de diálogo contraseña y, a continuación, haga clic en **siguiente**.  
  
    > [!WARNING]  
    > PDW de SQL Server no admite el carácter de signo de dólar ($) en las contraseñas de administrador de dominio o de administrador local. Una contraseña que contiene un signo de dólar será válida y podrá ser utilizable, pero puede bloquear las actividades de actualización y mantenimiento.  
  
    Confirme la descripción del nuevo usuario y, a continuación, haga clic en **Finalizar**.  
  
5.  En la lista de usuarios, haga doble clic en el nuevo usuario para abrir el cuadro de diálogo Propiedades de usuario.  
  
6.  En la ficha **Miembro de**, haga clic en **Agregar**.  
  
    Escriba **Admins. del dominio; PdwControlNodeAccess** y, a continuación, haga clic en **Comprobar nombres**. Haga clic en **OK**.  
  
    Esto agrega el nuevo usuario al grupo **Admins** . del dominio y al grupo **PdwControlNodeAccess** . Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)  
  
