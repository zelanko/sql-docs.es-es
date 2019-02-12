---
title: 'Nueva asignación de roles de sistema: Editar página de asignaciones de rol de sistema (Administrador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7c1354228c1afbebe519a94d16973d024b84caac
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032396"
---
# <a name="new-system-role-assignments-edit-system-role-assignments-page-report-manager"></a>Nueva asignación de roles de sistema: Editar página de asignaciones de rol de sistema (Administrador de informes)
  Use la página Nueva asignación de roles del sistema o Editar asignaciones de roles del sistema para definir la seguridad del servidor de informes. Toda la seguridad se define a través de asignaciones de roles, que asocian usuarios o grupos específicos a las tareas que pueden realizar. La lista de tareas se presenta como una definición de roles que se selecciona cuando se realiza una asignación de roles.  
  
 Las asignaciones de roles que se crean o modifican en el nivel de sistema se aplican al servidor de informes como un conjunto. Por ejemplo, la posibilidad de crear programaciones compartidas se especifica en el nivel de sistema porque estas programaciones se utilizan en todo el sistema.  
  
 De forma predeterminada, Reporting Services proporciona dos roles del nivel de sistema predefinidos:  
  
-   Usuario del sistema incluye tareas que permiten a los usuarios ver las propiedades del servidor de informes y las programaciones compartidas, así como ejecutar definiciones de informe con las que los usuarios pueden ver los informes click-through que se han publicado en el servidor de informes. A la mayoría de los usuarios deberían asignarse este rol.  
  
-   El Administrador del sistema incluye tareas para crear y administrar programaciones compartidas, establecer las propiedades del servidor y crear asignaciones de roles de nivel de sistema para otros usuarios. Pocos usuarios requieren permisos en este nivel.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-new-system-role-assignments-or-edit-system-role-assignments-page"></a>Para abrir la página Nueva asignación de roles del sistema o Editar asignaciones de roles del sistema  
  
1.  Abra el Administrador de informes.  
  
2.  En la esquina superior derecha, haga clic en **Configuración del sitio**. Esto abre la página de propiedades General del sitio.  
  
3.  Seleccione la pestaña **Seguridad** . Debe tener los permisos Administrador de contenido y Administrador del sistema para tener acceso a esta página.  
  
4.  Para crear una nueva asignación de roles, haga clic en **Nueva asignación de roles** en la barra de herramientas. Para editar una asignación de roles existente, haga clic en **Editar** junto a un grupo o usuario en la página de propiedades Seguridad.  
  
## <a name="options"></a>Opciones  
 **Grupo o usuario**  
 Escriba el nombre de una cuenta de usuario o grupo de su dominio. Si el servidor de informes se ejecuta con una cuenta local, debe especificar usuarios o grupos locales. Si el servidor de informes se ejecuta con una cuenta de dominio, debe especificar usuarios o grupos de dominio. Escriba la cuenta con este formato: \<dominio >\\< cuenta\>.  
  
> [!NOTE]  
>  Este cuadro solo está disponible en la página Nueva asignación de roles.  
  
 **Roles**  
 Proporciona una lista de roles del nivel del sistema que puede asignar a otros usuarios. Puede especificar varios roles para una asignación de roles única.  
  
 El Administrador de informes no muestra las tareas en cada rol ni proporciona una manera de agregar o modificar las tareas. Debe usar los roles como se definen. Para crear, modificar o eliminar roles, use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Para más información, consulte [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
 Tenga en cuenta que si está usando [!INCLUDE[ssExpressEd2005](../includes/ssexpressed2005-md.md)] con Advanced Services, debe usar los roles predeterminados proporcionados.  
  
 **Descripciones**  
 Muestra información adicional sobre el rol. En el caso de los roles predefinidos, como Usuario del sistema o Administrador del sistema, la descripción es un resumen de las tareas que admite cada rol.  
  
 **Eliminar asignación de roles**  
 Haga clic para eliminar una asignación de roles existente correspondiente a un usuario o a un grupo. Una asignación de roles no se puede eliminar si es la única que queda, ya que cada elemento debe tener, como mínimo, una asignación de roles.  
  
> [!NOTE]  
>  Este botón solo está disponible en la página Editar asignación de roles.  
  
## <a name="see-also"></a>Vea también  
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Asignaciones de roles](security/role-assignments.md)   
 [Definiciones de roles](security/role-definitions.md)  
  
  
