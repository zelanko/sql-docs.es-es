---
title: 'Analysis Services lección 11 del tutorial: Creación de roles | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6466eca2be66a20dfcab23f2097b71a2d0fc1cec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148946"
---
# <a name="create-roles"></a>Crear roles

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará roles. Los roles proporcionan seguridad de datos y objetos de base de datos de modelo limitando el acceso únicamente a aquellos usuarios que son miembros del rol. Cada rol se define con un solo permiso: Ninguno, lectura, lectura y proceso, proceso o administrador. Los roles se pueden definir durante la creación del modelo mediante el rol de administrador. Una vez implementado un modelo, puede administrar roles mediante SQL Server Management Studio (SSMS). Para obtener más información, consulte [Roles](../tabular-models/roles-ssas-tabular.md).
  
> [!NOTE]  
> No es necesario crear roles para completar este tutorial. De forma predeterminada, la cuenta que actualmente ha iniciado sesión tiene privilegios de administrador en el modelo. Sin embargo, para otros usuarios de su organización examinar mediante un cliente de informes, debe crear al menos un rol con la lectura de permisos y agregar esos usuarios como miembros.  
  
Cree tres roles:  
  
-   **Director de ventas** : este rol puede incluir a los usuarios de su organización para la que desea tener permiso para todos los objetos de modelo y datos de lectura.  
  
-   **Analista de ventas EE. UU.** : este rol puede incluir a los usuarios de su organización para que solo desea ser capaz de examinar los datos relacionados con las ventas en Estados Unidos. Para este rol, utilice una fórmula DAX para definir un *filtro de fila*, que restringe los miembros para examinar los datos solo para Estados Unidos.  
  
-   **Administrador** : este rol puede incluir los usuarios para el que quiera tener permisos de administrador, lo que permite acceso ilimitado y permisos para realizar tareas administrativas en la base de datos de modelo.  
  
Dado que las cuentas de usuario y grupo de Windows de su organización son únicas, puede agregar cuentas de su propia organización a los miembros. Sin embargo, para este tutorial, también puede dejar los miembros en blanco. Probar el efecto de cada rol más adelante en la lección 12: Analizar en Excel.  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 10: Crear particiones](../tutorial-tabular-1400/as-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Crear roles  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Para crear un rol de usuario Administrador de ventas  
  
1.  En el Explorador de modelos tabulares, haga clic en **Roles** > **Roles**.  
  
2.  En el Administrador de roles, haga clic en **New**.  
  
3.  Haga clic en el nuevo rol y, a continuación, en el **nombre** columna, cambiar el nombre del rol a **jefe de ventas**.  
  
4.  En la columna **Permisos** , haga clic en la lista desplegable y, después, seleccione el permiso **Lectura** . 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  Opcional: Haga clic en el **miembros** pestaña y, a continuación, haga clic en **agregar**. En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Para crear un rol de usuario Analista de ventas EE. UU.  
  
1.  En el Administrador de roles, haga clic en **New**.    
  
2.  Cambiar el nombre de la función para **analista de ventas EE. UU.**  
  
3.  Asigne a este rol **lectura** permiso.  
  
4.  Haga clic en la pestaña Filtros de fila y, a continuación, para la **DimGeography** tabla solo, en la columna filtro DAX, escriba la siguiente fórmula:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Una fórmula de filtro de fila se debe resolver como un valor booleano (TRUE o FALSE). Con esta fórmula, está especificando que solo las filas con el valor del código de región del país "US" son visibles para el usuario.  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  Opcional: Haga clic en el **miembros** pestaña y, a continuación, haga clic en **agregar**. En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol.  
  
#### <a name="to-create-an-administrator-user-role"></a>Para crear un rol de usuario de administrador  
  
1.  Haga clic en **Nueva**.  
  
2.  Cambiar el nombre del rol a **administrador**.  
  
3.  Asigne a este rol **administrador** permiso.  
  
4.  Opcional: Haga clic en el **miembros** pestaña y, a continuación, haga clic en **agregar**. En el cuadro de diálogo **Seleccionar usuario o grupo** , especifique los usuarios o grupos de Windows de su organización que quiera incluir en el rol. 
  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 12: Analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).

  
  
