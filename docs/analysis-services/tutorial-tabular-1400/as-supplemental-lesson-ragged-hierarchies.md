---
title: 'Lección complementaria de Analysis Services tutorial: jerarquías desiguales | Documentos de Microsoft'
description: Describe cómo corregir las jerarquías desiguales en el tutorial de Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0ab9620add67094ac4115ea670c08328d7c075de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lección complementaria - jerarquías desiguales

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección complementaria, resolver un problema común al dinamizar en jerarquías que contengan valores en blanco (miembros) en distintos niveles. Por ejemplo, una organización donde un director de alto nivel tiene tanto directores de departamento como no administradores como subordinados directos. O bien, jerarquías geográficas formada por país-ciudad, donde algunas ciudades no tienen un elemento primario estado o provincia, como Washington D.C., ciudad del Vaticano. Cuando una jerarquía tiene miembros en blanco, a menudo se desciende en niveles diferentes o desiguales.

![As-Lesson-Detail-ragged-Hierarchies-Table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

Los modelos tabulares en el nivel de compatibilidad de 1400 tienen más **ocultar miembros** propiedad para las jerarquías. El **predeterminado** configuración supone que no hay ningún miembro en blanco en cualquier nivel. El **ocultar miembros en blanco** configuración excluye los miembros en blanco de la jerarquía cuando se agrega a una tabla dinámica o informe.  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
En este artículo de lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar las tareas de esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado. 

Si ha creado el proyecto AW Internet Sales como parte del tutorial, el modelo no contiene aún los datos o jerarquías desiguales. Para completar esta lección complementaria, primero debe crear el problema mediante la adición de algunas tablas adicionales, crear relaciones, columnas calculadas, una medida y una nueva jerarquía de organización. Esa parte tarda unos 15 minutos. A continuación, obtendrá solucionar en tan solo unos minutos.  

## <a name="add-tables-and-objects"></a>Agregar tablas y objetos
  
### <a name="to-add-new-tables-to-your-model"></a>Para agregar nuevas tablas al modelo
  
1.  En el Explorador de modelos tabulares, expanda **orígenes de datos**, a continuación, haga clic en la conexión > **importar nuevas tablas**.
  
2.  En el navegador, seleccione **DimEmployee** y **FactResellerSales**y, a continuación, haga clic en **Aceptar**.

3.  En el Editor de consultas, haga clic en **importación**

4.  Cree el siguiente [relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | tabla 1           | Columna       | Dirección del filtro   | tabla 2     | Columna      | Activo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Predeterminado            | DimDate     | Date        | Sí    |
    | FactResellerSales | DueDate      | Predeterminado            | DimDate     | Date        | no     |
    | FactResellerSales | ShipDateKey  | Predeterminado            | DimDate     | Date        | no     |
    | FactResellerSales | ProductKey   | Predeterminado            | DimProduct  | ProductKey  | Sí    |
    | FactResellerSales | EmployeeKey  | En ambas tablas | DimEmployee | EmployeeKey | Sí    |

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

6.  En el **DimEmployee** de tabla, cree un [jerarquía](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) denominado **organización**. Agregue el columnas siguientes en el orden: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  En el **FactResellerSales** de tabla, cree el siguiente [medida](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) para abrir Excel y crear automáticamente una tabla dinámica.

9.  En **PivotTable Fields**, agregue el **organización** jerarquía desde el **DimEmployee** tabla a **filas**y el  **ResellerTotalSales** medida desde la **FactResellerSales** tabla a **valores**.

    ![As-Lesson-Detail-ragged-Hierarchies-PivotTable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Como puede ver en la tabla dinámica, la jerarquía muestra las filas que son desiguales. Hay muchas filas donde se muestran los miembros en blanco.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Para corregir la jerarquía desigual estableciendo los miembros de ocultar propiedad

1.  En **Explorador de modelos tabulares**, expanda **tablas** > **DimEmployee** > **jerarquías**  >  **Organización**.

2.  En **propiedades** > **ocultar miembros**, seleccione **ocultar miembros en blanco**. 

    ![As-Lesson-Detail-ragged-Hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  En Excel, actualizar la tabla dinámica. 

    ![As-Lesson-Detail-ragged-Hierarchies-PivotTable-Refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Ahora se ve mucho mejor.

## <a name="see-also"></a>Vea también   
[Lección 9: Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Lección complementaria - seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lección complementaria - filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
