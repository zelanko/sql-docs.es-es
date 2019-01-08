---
title: Crear un administrador de dominio - Analytics Platform System | Microsoft Docs
description: Algunas operaciones requieren privilegios de administrador de dominio de Analytics Platform System. Esto explica cómo crear administradores de dominio de aplicación adicionales.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 852fb3c6cee7c65f8799102bbd65ab368cd0d9e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538579"
---
# <a name="create-an-aps-domain-administrator"></a>Crear un administrador de dominio APS
Algunas operaciones requieren privilegios de administrador de dominio de Analytics Platform System. Esto explica cómo crear administradores de dominio de aplicación adicionales.  
  
## <a name="create-a-domain-administrator"></a>Crear un administrador de dominio  
Tener permisos suficientes para configurar todos los nodos APS, el usuario que ejecuta el **APS Configuration Manager** (`dwconfig.exe`) debe ser un miembro de la **Admins. del dominio** grupo. Para iniciar y detener los servicios de puntos de acceso, el usuario debe ser un miembro de la **PdwControlNodeAccess** grupo.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Para agregar un usuario al grupo Admins. del dominio  
  
1.  Inicie sesión en el nodo activo de AD **(_dispositivo\_dominio_-AD01** o  **_dispositivo\_dominio_-AD02**) uso de una cuenta de administrador de dominio de aplicación existente.  
  
2.  En el menú Iniciar, haga clic en **Ejecutar**. En el **abierto** , escriba **dsa.msc**. Haga clic en **Aceptar**.  
  
3.  En el **equipos y usuarios de Active Directory** de programa, haga clic en **usuarios**, apunte a **New**y, a continuación, haga clic en **usuario**.  
  
4.  En el **nuevo objeto - usuario** cuadro de diálogo, complete la descripción del nuevo usuario y, a continuación, haga clic en **siguiente**.  
  
    Complete el cuadro de diálogo de contraseña y, a continuación, haga clic en **siguiente**.  
  
    > [!WARNING]  
    > PDW de SQL Server no admite el carácter de signo de dólar ($) en el Administrador de dominio o las contraseñas de administrador local. Una contraseña que contenga un signo de dólar válida y se puede usar pero puede bloquear las actividades de actualización y mantenimiento  
  
    Confirme la nueva descripción de usuario y, a continuación, haga clic en **finalizar**.  
  
5.  En la lista de usuarios, haga doble clic en el nuevo usuario para abrir el cuadro de diálogo de propiedades de usuario.  
  
6.  En el **miembro de** , haga clic **agregar**.  
  
    Tipo **Admins. del dominio; PdwControlNodeAccess** y, a continuación, haga clic en **comprobar nombres**. Haga clic en **Aceptar**.  
  
    Esto agrega el nuevo usuario a la **Admins. del dominio** grupo y la **PdwControlNodeAccess** grupo. Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
