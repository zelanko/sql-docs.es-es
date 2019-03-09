---
title: 'Analysis Services lección complementaria del tutorial: Jerarquías desiguales | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 39f8bcc63b7e5344f70a6d4a3b6c44ae3e69e108
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685404"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lección complementaria: Jerarquías desiguales

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección complementaria, resolverá un problema común al dinamizar en jerarquías que contienen valores en blanco (miembros) en distintos niveles. Por ejemplo, una organización donde un director de alto nivel tiene tanto directores de departamento como no directores como subordinados directos. O bien, las jerarquías geográficas formadas país-región-ciudad, donde algunas ciudades no tienen un elemento primario estado o provincia, como Washington D.C., ciudad del Vaticano. Cuando una jerarquía tiene miembros en blanco, a menudo desciende en niveles diferentes o desiguales.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

Los modelos tabulares en el nivel de compatibilidad 1400 tienen más **ocultar miembros** propiedad para las jerarquías. El **predeterminado** configuración asume que no hay ningún miembro en blanco en cualquier nivel. El **ocultar miembros en blanco** configuración excluye los miembros en blanco de la jerarquía cuando se agrega a una tabla dinámica o informe.  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
En este artículo de la lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar las tareas de esta lección complementaria, debe haber completado todas las lecciones anteriores o tiene un proyecto de modelos de ejemplo Adventure Works Internet Sales completado. 

Si ha creado el proyecto AW Internet Sales como parte del tutorial, el modelo no tiene todavía ningún dato ni jerarquías desiguales. Para completar esta lección complementaria, primero debe crear el problema agregando algunas tablas, crear relaciones, columnas calculadas, una medida y una nueva jerarquía de organización. Solo tardará unos 15 minutos. A continuación, podrá solucionar el problema en cuestión de minutos.  

## <a name="add-tables-and-objects"></a>Agregar tablas y objetos
  
### <a name="to-add-new-tables-to-your-model"></a>Para agregar nuevas tablas al modelo
  
1.  En el Explorador de modelos tabulares, expanda **orígenes de datos**, a continuación, haga clic en la conexión > **importar nuevas tablas**.
  
2.  En el navegador, seleccione **DimEmployee** y **FactResellerSales**y, a continuación, haga clic en **Aceptar**.

3.  En el Editor de consultas, haga clic en **importación**

4.  Cree la siguiente [relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | tabla 1           | columna       | Dirección del filtro   | tabla 2     | columna      | Activo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Default            | DimDate     | date        | Sí    |
    | FactResellerSales | DueDate      | Default            | DimDate     | date        | No     |
    | FactResellerSales | ShipDateKey  | Default            | DimDate     | date        | No     |
    | FactResellerSales | ProductKey   | Default            | DimProduct  | ProductKey  | Sí    |
    | FactResellerSales | EmployeeKey  | Ambas tablas | DimEmployee | EmployeeKey | Sí    |

5. En el **DimEmployee** de tabla, cree el siguiente [columnas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **Ruta de acceso** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  En el **DimEmployee** de tabla, cree un [jerarquía](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) denominado **organización**. Agregue las columnas siguientes en el orden: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  En el **FactResellerSales** de tabla, cree el siguiente [medida](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) para abrir Excel y crear automáticamente una tabla dinámica.

9.  En **PivotTable Fields**, agregar el **organización** jerarquía desde el **DimEmployee** tabla **filas**y el  **ResellerTotalSales** medida desde la **FactResellerSales** tabla **valores**.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Como puede ver en la tabla dinámica, la jerarquía muestra filas desiguales. Hay muchas filas donde se muestran los miembros en blanco.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Para corregir la jerarquía desigual estableciendo los miembros de ocultar, propiedad

1.  En **Explorador de modelos tabulares**, expanda **tablas** > **DimEmployee** > **jerarquías**  >  **Organización**.

2.  En **propiedades** > **ocultar miembros**, seleccione **ocultar miembros en blanco**. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  En Excel, actualice la tabla dinámica. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    ¡Ahora se ve mucho mejor!

## <a name="see-also"></a>Vea también   
[Lección 9: Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Lección complementaria: seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lección complementaria: filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
