---
title: 'Lección 12: crear roles | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec4bad8ef036e8f19ce0a856f3d9c04bafd0e7c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079267"
---
# <a name="lesson-12-create-roles"></a>Lección 12: Crear roles
  En esta lección, creará roles. Los roles proporcionan seguridad a los objetos y datos de la base de datos del modelo limitando el acceso únicamente a los usuarios de Windows que sean miembros del rol. Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y procesamiento, Procesamiento o Administrador. Los roles se pueden definir durante la creación del modelo mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Una vez implementado un modelo, los roles se pueden administrar con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Roles &#40;SSAS tabular&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  No es necesario crear roles para completar este tutorial. De forma predeterminada, la cuenta en la que ha iniciado sesión actualmente tendrá privilegios de administrador en el modelo. Sin embargo, para permitir que otros usuarios de su organización examinen el modelo utilizando una aplicación cliente de informes, debe crear al menos un rol con permisos de lectura y agregar esos usuarios como miembros.  
  
 Creará tres roles:  
  
-   Jefe de ventas: este rol puede incluir a los usuarios de la organización para los que desea tener permiso de lectura para todos los objetos y datos del modelo.  
  
-   Analista de ventas EE. UU.: este rol puede incluir a los usuarios de su organización para los que desea que solo puedan examinar los datos relacionados con las ventas en EE. UU. (Estados Unidos). Para este rol, usará una fórmula DAX para definir un *filtro de fila* que hace que los miembros solo puedan examinar los datos de Estados Unidos.  
  
-   Administrador: este rol puede incluir a los usuarios para los que desea tener permiso de administrador, lo que permite el acceso ilimitado y permisos para realizar tareas administrativas en la base de datos modelo.  
  
 Dado que las cuentas de usuario y de grupo de Windows de la organización son únicas, puede agregar cuentas de su propia organización a los miembros, Pero para este tutorial también puede dejar los miembros en blanco. Podrá probar el efecto de cada rol más adelante en la Lección 12: Analizar en Excel.  
  
 Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 11: Crear particiones](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Crear roles  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para crear el rol de usuario Director de ventas  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
     Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, a continuación, en la columna **nombre** , cambie el `Internet Sales Manager`nombre del rol a.  
  
4.  En la columna **Permisos**, haga clic en la lista desplegable y, luego, seleccione el permiso **Lectura**.  
  
5.  Opcional: Haga clic en la pestaña **Miembros** y, luego, haga clic en **Agregar**.  
  
6.  En el cuadro de diálogo **Seleccionar usuarios o grupos**, escriba los usuarios o grupos de Windows de la organización que quiere incluir en el rol.  
  
7.  Compruebe las selecciones y, a continuación, haga clic en **Aceptar** .  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para crear el rol de usuario Analista de ventas de EE. UU.  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
     Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, a continuación, en la columna **nombre** , cambie el `Internet Sales US`nombre del rol a.  
  
4.  En la columna **Permisos**, haga clic en la lista desplegable y, luego, seleccione el permiso **Lectura**.  
  
5.  Haga clic en la pestaña Filtros de fila y, después, solo para la tabla **Geografía** , en la columna de Filtro DAX, escriba la siguiente fórmula:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Una fórmula de filtro de fila debe resolverse en un valor booleano (TRUE/FALSE). Con esta fórmula, está especificando que solo las filas con el valor de código de región del país "EE. UU." estarán visibles para el usuario.  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
6.  Opcional: Haga clic en la pestaña **Miembros** y, luego, haga clic en **Agregar**.  
  
7.  En el cuadro de diálogo **Seleccionar usuarios o grupos**, escriba los usuarios o grupos de Windows de la organización que quiere incluir en el rol.  
  
8.  Compruebe las selecciones y, a continuación, haga clic en **Aceptar** .  
  
#### <a name="to-create-an-administrator-role"></a>Para crear un rol Administrador  
  
1.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
2.  Haga clic en el nuevo rol y, a continuación, en la columna **nombre** , cambie el `Internet Sales Administrator`nombre del rol a.  
  
3.  En la columna **Permisos** , haga clic en la lista desplegable y luego seleccione el permiso **Administrador** .  
  
4.  Haga clic en la pestaña **Miembros** y luego en **Agregar**.  
  
5.  Opcional: En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
6.  Compruebe las selecciones y, a continuación, haga clic en **Aceptar** .  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 13: Analizar en Excel](lesson-12-analyze-in-excel.md).  
  
  
