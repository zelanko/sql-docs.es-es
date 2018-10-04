---
title: 'Lección 12: Creación de Roles | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d3ca1e013ede0e8bd40c1ce5af36d44ea45122d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164085"
---
# <a name="lesson-12-create-roles"></a>Lección 12: Crear roles
  En esta lección, creará roles. Los roles proporcionan seguridad a los objetos y datos de la base de datos del modelo limitando el acceso únicamente a los usuarios de Windows que sean miembros del rol. Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y proceso, Proceso o Administrador. Los roles se pueden definir durante la creación del modelo mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Una vez implementado un modelo, los roles se pueden administrar con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Roles &#40;SSAS tabular&#41;](tabular-models/roles-ssas-tabular.md).  
  
> [!NOTE]  
>  No es necesario crear roles para completar este tutorial. De forma predeterminada, la cuenta con la que ha iniciado sesión tendrá privilegios Administrador para el modelo. Sin embargo, para permitir que otros usuarios de su organización examinen el modelo utilizando una aplicación cliente de informes, debe crear al menos un rol con permisos de lectura y agregar esos usuarios como miembros.  
  
 Creará tres roles:  
  
-   Jefe de ventas: este rol puede incluir a los usuarios de la organización a los que desea otorgar permiso de lectura para todos los objetos y datos del modelo.  
  
-   Analista de ventas EE. UU.: este rol puede incluir a los usuarios de la organización que desea que solo puedan examinar los datos relacionados con las ventas en EE. UU. Para este rol, usará una fórmula DAX para definir un *Filtro de fila*, que restringe los miembros para que solo examinen los datos correspondientes a Estados Unidos.  
  
-   Administrador: este rol puede incluir a los usuarios a los que desea otorgar el permiso Administrador, que permite acceso y permisos ilimitados para realizar tareas administrativas en la base de datos del modelo.  
  
 Dado que las cuentas de usuario y grupo de Windows de su organización son únicas, puede agregar cuentas de su propia organización a los miembros. Sin embargo, para este tutorial, también puede dejar los miembros en blanco. Todavía podrá probar el efecto de cada rol más adelante en la lección 12: Analizar en Excel.  
  
 Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 11: Crear particiones](lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Crear roles  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para crear un rol de usuario Administrador de ventas  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
     Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, a continuación, en el **nombre** columna, cambiar el nombre de la función para `Internet Sales Manager`.  
  
4.  En la columna **Permisos** , haga clic en la lista desplegable y, después, seleccione el permiso **Lectura** .  
  
5.  Opcional: Haga clic en la pestaña **Miembros** y, después, en **Agregar**.  
  
6.  En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
7.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para crear un rol de usuario Analista de ventas EE. UU.  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, luego, en **Roles**.  
  
2.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
     Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, a continuación, en el **nombre** columna, cambiar el nombre de la función para `Internet Sales US`.  
  
4.  En la columna **Permisos** , haga clic en la lista desplegable y, después, seleccione el permiso **Lectura** .  
  
5.  Haga clic en la pestaña Filtros de fila y, después, solo para la tabla **Geografía** , en la columna de Filtro DAX, escriba la siguiente fórmula:  
  
     `=Geography[Country Region Code] = "US"`  
  
     Una fórmula de filtro de fila se debe resolver como un valor booleano (TRUE o FALSE). Con esta fórmula, está especificando que solo las filas con el valor de código de país o región de "US" estarán visibles para el usuario.  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
6.  Opcional: Haga clic en la pestaña **Miembros** y, después, en **Agregar**.  
  
7.  En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
8.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
#### <a name="to-create-an-administrator-role"></a>Para crear un rol Administrador  
  
1.  En el cuadro de diálogo **Administrador de roles** , haga clic en **Nuevo**.  
  
2.  Haga clic en el nuevo rol y, a continuación, en el **nombre** columna, cambiar el nombre de la función para `Internet Sales Administrator`.  
  
3.  En la columna **Permisos** , haga clic en la lista desplegable y luego seleccione el permiso **Administrador** .  
  
4.  Haga clic en la pestaña **Miembros** y luego en **Agregar**.  
  
5.  Opcional: En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
6.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 13: Analizar en Excel](lesson-12-analyze-in-excel.md).  
  
  
