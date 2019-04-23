---
title: Página de propiedades de seguridad, elementos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bb1835a67ca1f909bf382fd227783cb0a20bbbf5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934771"
---
# <a name="security-properties-page-items-report-manager"></a>Página de propiedades de seguridad, elementos (Administrador de informes)
  Use la página Propiedades de seguridad para ver o modificar la configuración de seguridad que determina el acceso a carpetas, informes, modelos, recursos y orígenes de datos compartidos. Esta página está disponible para los elementos para los que tenga permiso de protección.  
  
 El acceso a los elementos se define a través de asignaciones de roles, que especifican las tareas que puede realizar un grupo o usuario. Una asignación de roles consta de un nombre de usuario o grupo y de una o varias definiciones de roles que especifican un conjunto de tareas.  
  
 La configuración de seguridad se hereda de la carpeta raíz a las subcarpetas y los elementos que contienen. A menos que se anule explícitamente la herencia de la seguridad, las subcarpetas y los elementos heredan el contexto de seguridad de un elemento primario. Si se redefine una directiva de seguridad para una carpeta situada en la mitad de la jerarquía, todos los elementos secundarios, incluidas las subcarpetas, adoptarán la nueva configuración de seguridad.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-security-page-for-an-item"></a>Para abrir la página Seguridad de un elemento  
  
1.  Abra el Administrador de informes y busque el elemento para el que desea establecer la configuración de seguridad.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, efectúe uno de los pasos siguientes:  
  
    -   Haga clic en **Seguridad**. Se abrirá la página de propiedades Seguridad para el elemento.  
  
    -   Haga clic en **Administrar** para abrir la página de propiedades General del elemento. A continuación, seleccione la pestaña **Seguridad** .  
  
 **Editar seguridad del elemento**  
 Haga clic para cambiar la manera en la que se define la seguridad para el elemento actual. Si va a modificar la seguridad de una carpeta, los cambios se aplicarán al contenido de la carpeta actual y a todas sus subcarpetas.  
  
 Este botón no está disponible para la carpeta Inicio.  
  
 Los botones siguientes están disponibles cuando se edita la seguridad de un elemento.  
  
 **Eliminar**  
 Active la casilla situada al lado del nombre de usuario o grupo que desea eliminar y haga clic en **Eliminar**. No se puede eliminar una asignación de roles si es la única que queda o si es una asignación de roles integrada, como "Built-in\Administradores", que define la línea base de la seguridad del servidor de informes. Si se elimina una asignación de roles, no se elimina la cuenta de usuario o grupo ni las definiciones de roles.  
  
 **Nueva asignación de roles**  
 Haga clic para abrir la página Nueva asignación de roles, que se usa para crear más asignaciones de roles para el elemento actual. Para obtener más información, consulte [nueva asignación de roles: Editar página de asignación de rol &#40;el Administrador de informes&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md).  
  
 **Volver a la seguridad del elemento primario**  
 Haga clic para restablecer la configuración de seguridad a la de la carpeta primaria inmediata. Si la herencia permanece intacta en toda la jerarquía de carpetas del servidor de informes, se utiliza la configuración de seguridad de la carpeta de nivel superior, Inicio.  
  
 **Grupo o usuario**  
 Muestra los grupos y usuarios que forman parte de una asignación de roles existente para el elemento actual. Se han definido las asignaciones de roles existentes para la carpeta actual de los grupos y usuarios que se muestran en esta columna. Puede hacer clic en un nombre de usuario o grupo para ver o editar los detalles de las asignaciones de roles.  
  
 **Roles**  
 Muestra una o varias definiciones de roles que son parte de una asignación de roles existente. Si se asignan varios roles a una cuenta de usuario o grupo, ese usuario o grupo puede realizar todas las tareas que pertenecen a todos esos roles. Para ver las tareas asociadas a un rol, use SQL Server Management Studio para ver las tareas de cada definición de rol.  
  
## <a name="see-also"></a>Vea también  
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Roles predefinidos](security/role-definitions-predefined-roles.md)   
 [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Asignaciones de roles](security/role-assignments.md)   
 [Definiciones de roles](security/role-definitions.md)  
  
  
