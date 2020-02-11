---
title: 'Lección 10: crear jerarquías | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb70d7d495d88ee62e98bf27f2b92bf569c98387
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078189"
---
# <a name="lesson-10-create-hierarchies"></a>Lección 10: Crear jerarquías
  En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía geografía puede tener subniveles de país, estado, provincia y ciudad. Las jerarquías pueden aparecer separadas de otras columnas en una lista de campos de aplicación cliente de generación de informes, lo que facilita que los usuarios puedan navegar por ellas e incluirlas en un informe. Para obtener más información, vea [Jerarquías &#40;SSAS tabular&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Para crear jerarquías, usará el diseñador de modelos en *Vista de diagrama*. La creación y administración de jerarquías no se admite en la vista de datos del diseñador de modelos.  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 9: Crear perspectivas](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Crear jerarquías  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Para crear una jerarquía Categoría en la tabla Product  
  
1.  En el diseñador de modelos, haga clic `Model` en el menú, elija **vista de modelo**y, a continuación, haga clic en **vista de diagrama**.  
  
    > [!TIP]  
    >  Utilice los controles de Minimapa situados en la parte superior derecha del diseñador de modelos para cambiar el modo en que se muestran los objetos en la vista de diagrama. Si cambia la posición de los objetos en la vista de diagrama, esa vista se conservará cuando guarde el proyecto.  
  
2.  En el diseñador de modelos, haga clic con `Product` el botón secundario en la tabla y, a continuación, haga clic en **crear jerarquía**. Aparece una nueva jerarquía en la parte inferior de la ventana de tabla.  
  
3.  En el nombre de la jerarquía, cambie el nombre de `Category`la jerarquía; para ello, escriba y, a continuación, presione Entrar.  
  
4.  En la `Product` tabla, haga clic en la columna **Product Category Name** , arrástrela a `Category` la jerarquía y suelte el `Category` nombre.  
  
5.  En la `Category` jerarquía, haga clic con el botón secundario en la columna **Product Category Name** , haga clic en `Category`cambiar **nombre**y, a continuación, escriba.  
  
    > [!NOTE]  
    >  Al cambiar el nombre de una columna de una jerarquía no cambia el nombre de esa columna en la tabla. Una columna de una jerarquía es simplemente una representación de la columna en la tabla.  
  
6.  En la `Product` tabla, haga clic con el botón secundario en la columna **Product subcategory Name** , en el menú contextual, seleccione **Agregar a jerarquía**y, a continuación, haga clic en `Category`.  
  
7.  Cambie el nombre de la subcategoría `Subcategory`de **producto** a.  
  
8.  Con hacer clic y arrastrar, o mediante el comando **Agregar a la jerarquía** en el menú contextual, agregue las columnas **nombre del modelo** y **nombre del producto** (en orden) y colóquelas debajo de la columna Nombre de **subcategoría del producto** . Cambie el nombre de `Model` estas `Product`columnas y, respectivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Para crear jerarquías en la tabla Date  
  
1.  En el diseñador de modelos, haga clic con el botón derecho en la tabla **Fecha** y, después, haga clic en **Crear jerarquía**.  
  
2.  Cambie el nombre de la jerarquía a **Calendario**.  
  
3.  Agregue las columnas siguientes, en orden, y después cámbieles el nombre:  
  
    |Columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año del calendario|Year|  
    |Semestre del calendario|Semestre|  
    |Trimestre del calendario|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Día|  
  
4.  En la tabla **Fecha** , repita los pasos anteriores y cree una jerarquía **Fiscal** que incluya las siguientes columnas:  
  
    |Columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año fiscal|Year|  
    |Semestre fiscal|Semestre|  
    |Trimestre fiscal|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Día|  
  
5.  Finalmente, en la tabla **Fecha** , repita los pasos anteriores y cree una jerarquía **Calendario de producción** que incluya las columnas siguientes:  
  
    |Columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año del calendario|Year|  
    |Week Number Of Year|Semana|  
    |Day Of Week|Día|  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 11: Crear particiones](lesson-10-create-partitions.md).  
  
  
