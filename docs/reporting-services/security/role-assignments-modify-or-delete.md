---
title: Modificación o eliminación de una asignación de roles (portal web de SSRS) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b944ca316825e65ce2d1854709e0a08ce1fd1cb8
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449624"
---
# <a name="role-assignments---modify-or-delete"></a>Asignaciones de roles: modificación o eliminación

Una asignación de roles asigna una cuenta de usuario o grupo a un rol predefinido que define las tareas que se pueden realizar. Determina los tipos de tareas que un usuario realiza en una carpeta, informe, modelo u otro tipo de contenido. Para crear, modificar o eliminar asignaciones de roles, use el portal web de SSRS. Después de crear una asignación de roles para un grupo o usuario concreto, puede modificarla posteriormente seleccionando un rol diferente. Si desea revocar los permisos a un servidor de informes, puede eliminar una asignación de roles del servidor de informes.  

Dependiendo de su objetivo, los enfoques alternativos podrían ser más adecuados. Entre los ejemplos se incluyen la personalización o la creación de una nueva definición de roles, o la modificación de la pertenencia de una cuenta de grupo en Active Directory.  

Por ejemplo, supongamos que tiene un grupo de usuarios que necesitan administrar su contenido, pero que no deberían tener el conjunto completo de permisos asociado al Administrador de contenido. Podría crear una definición de roles denominada Administrador de contenido del departamento. Podría incluir todas las tareas en el Administrador de contenido, excepto la **definición de las directivas de seguridad de los elementos**.

De forma similar, si es un administrador del sistema o de red, probablemente le resulte más fácil administrar las cuentas de grupo de Active Directory que las asignaciones de roles en el portal web. Puede reducir la sobrecarga de administrar las asignaciones de roles mediante la creación de una asignación de roles única para una cuenta de grupo. A continuación, puede modificar la pertenencia al grupo cuando los usuarios ya no necesitan acceso a los informes.
  
 Si determina que el mejor enfoque es la modificación o la eliminación de una asignación de roles, recuerde comprobar las asignaciones de roles del sistema y las asignaciones de roles de nivel de elemento. Cada tipo de asignación de roles se configura en páginas diferentes del portal web.
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>Para modificar o eliminar una asignación de roles del sistema
  
1. Acceda al [portal web de un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/web-portal-ssrs-native-mode.md).

2. Seleccione **Configuración del sitio** > **Seguridad**. Todas las asignaciones de roles del nivel de sistema definidas actualmente para el servidor o la implementación escalada aparecen enumeradas por nombre de cuenta.

3. Busque la asignación de rol que desea modificar o eliminar.

4. Para agregar o quitar el rol de un usuario o grupo determinado, seleccione **Editar**.

5. Para eliminar una asignación de rol, seleccione la casilla situada junto al nombre de usuario o grupo y, después, seleccione **Eliminar**.

### <a name="to-modify-or-delete-an-item-role-assignment"></a>Para modificar o eliminar una asignación de roles de elemento

1. Acceda al portal web y busque el elemento para el que desea modificar o eliminar una asignación de roles.

2. Mantenga el mouse sobre el elemento y seleccione la flecha de lista desplegable.

3. En el menú desplegable, seleccione **Seguridad**.

4. Busque la asignación de rol que desea modificar o eliminar.

5. Para agregar o quitar el rol de un usuario o grupo determinado, seleccione **Editar**.

6. Para eliminar una asignación de rol, seleccione la casilla situada junto al nombre de usuario o grupo y, después, seleccione **Eliminar**.

## <a name="see-also"></a>Vea también

[Creación y administración de asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md)  
[Asignaciones de roles](../../reporting-services/security/role-assignments.md)  
