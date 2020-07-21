---
title: Asignaciones de roles | Microsoft Docs
ms.date: 05/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a6fe3c0cd82d8ee8b92948d76d4f7cdb5fa4cf73
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570569"
---
# <a name="role-assignments"></a>Asignaciones de roles

En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], las *asignaciones de roles* determinan el acceso a los elementos almacenados y al propio servidor de informes. Una asignación de roles consta de las siguientes partes:  
  
- Un elemento protegible para el que desea controlar el acceso. Ejemplos de elementos protegibles son carpetas, informes y recursos.  
  
- Una cuenta de usuario o grupo que se pueda autenticar con seguridad de Windows u otro mecanismo de autenticación.  
  
- Las definiciones de roles definen un conjunto de tareas admisibles e incluyen:
  - **Browser**
  - **Administrador de contenido**
  - **Mis informes**
  - **Publicador**
  - **Generador de informes**
  - **Administrador del sistema**
  - **Usuario del sistema**

 Las asignaciones de roles se heredan dentro de la jerarquía de carpetas y, a su vez, las heredan de forma automática e independiente:

- **Informes**
- **Orígenes de datos compartidos**
- **Recursos**
- **Subcarpetas**

Al definir asignaciones de roles para elementos individuales, se puede reemplazar la seguridad heredada. Todas las partes de la jerarquía de carpetas deben estar protegidas por al menos una asignación de roles. No puede crear un elemento no protegido ni manipular la configuración de tal manera que produzca un elemento no protegido.  
  
 El siguiente diagrama muestra una asignación de roles que asigna un grupo y un usuario específico al rol **Publicador** para la carpeta B.  
  
 ![Diagrama de asignaciones de roles](../../reporting-services/security/media/report-securityarch.gif "Diagrama de asignaciones de roles")  
Diagrama de asignaciones de roles  
  
## <a name="system-level-and-item-level-role-assignments"></a>Asignaciones de roles de nivel de sistema y de nivel de elemento

 La seguridad basada en roles en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se organiza en los siguientes niveles:

- Las asignaciones de roles de nivel de elemento controlan el acceso a los elementos de la jerarquía de carpetas del servidor de informes, como:
  - reports
  - carpetas
  - Modelos de informe
  - orígenes de datos compartidos
  - otros recursos

- Estas asignaciones de roles se definen cuando se crea una asignación de roles para un elemento específico o la carpeta Inicio.

- Las asignaciones de roles del sistema autorizan operaciones cuyo ámbito es el servidor en su conjunto. Por ejemplo, la capacidad para administrar los trabajos es una operación a nivel del sistema. Una asignación de roles del sistema no es equivalente a un administrador del sistema. No confiere permisos avanzados que concedan control total de un servidor de informes.

Una asignación de roles del sistema no autoriza el acceso a elementos en la jerarquía de carpetas. La seguridad del sistema y la del elemento se excluyen mutuamente. Algunas veces, puede ser necesario crear una asignación de roles del sistema y una asignación de roles de nivel de elemento para proporcionar acceso suficiente a un usuario o grupo.

## <a name="users-and-groups-in-role-assignments"></a>Usuarios y grupos en asignaciones de roles

 Las cuentas de usuario o grupo que especifique en asignaciones de roles son cuentas de dominio. El servidor de informes hace referencia a usuarios y grupos de un dominio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, u otro modelo de seguridad si se usa una extensión de seguridad personalizada, pero no los crea ni los administra.

Entre todas las asignaciones de roles aplicables a un elemento determinado, no puede haber dos que especifiquen el mismo usuario o grupo. Si una cuenta de usuario también forma parte de una cuenta de grupo y tiene asignaciones de roles para ambas, el conjunto combinado de tareas para ambas asignaciones de roles está disponible para el usuario.

Si se agrega un usuario a un grupo que ya tiene una asignación de roles, debe restablecer Internet Information Services (IIS) para que la nueva asignación de roles surta efecto.

## <a name="predefined-role-assignments"></a>Asignaciones de roles predefinidos

 De manera predeterminada, las asignaciones de roles predefinidos se implementan para permitir a los administradores locales administrar el servidor de informes. Puede agregar asignaciones de roles adicionales para conceder acceso a otros usuarios.

 Para obtener más información sobre las asignaciones de roles predefinidos que proporcionan la seguridad predeterminada, vea [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md).  

## <a name="see-also"></a>Consulte también

 [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)

 [Modificar o eliminar una asignación de roles &#40; Portal web de SSRS &#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)

 [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)

 [Concesión de permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
