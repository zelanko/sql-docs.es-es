---
title: 'Lección 10: Crear jerarquías | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: ea741676f07020291c2aa94d130c2f595a50f323
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103433"
---
# <a name="lesson-10-create-hierarchies"></a>Lección 10: Crear jerarquías
  En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía Geografía puede tener subniveles para País, Provincia y Ciudad. Las jerarquías pueden aparecer por separado de otras columnas en una lista de campos de la aplicación cliente de informes, lo que facilita la navegación de los usuarios del cliente y su inclusión en un informe. Para obtener más información, vea [Jerarquías &#40;SSAS tabular&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Para crear jerarquías, usará el diseñador de modelos en *Vista de diagrama*. La creación y administración de jerarquías no se admite en la vista de datos del diseñador de modelos.  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 9: Crear perspectivas](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Crear jerarquías  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Para crear una jerarquía Categoría en la tabla Product  
  
1.  En el Diseñador de modelos, haga clic en el `Model` menú y, a continuación, seleccione **vista de modelo**y, a continuación, haga clic en **vista de diagrama**.  
  
    > [!TIP]  
    >  Utilice los controles de Minimapa situados en la parte superior derecha del diseñador de modelos para cambiar el modo en que se muestran los objetos en la vista de diagrama. Si cambia la posición de los objetos en la vista de diagrama, esa vista se conservará cuando guarde el proyecto.  
  
2.  En el Diseñador de modelos, haga clic en el `Product` de tabla y, a continuación, haga clic en **crear jerarquía**. Aparece una nueva jerarquía en la parte inferior de la ventana de tabla.  
  
3.  En el nombre de la jerarquía, el nombre de la jerarquía escribiendo `Category`, y, a continuación, presione ENTRAR.  
  
4.  En el `Product` de tabla, haga clic en el **Product Category Name** columna, a continuación, arrástrelo hasta el `Category` jerarquía y suelte el botón en la parte superior de la `Category` nombre.  
  
5.  En el `Category` jerarquía, haga clic en el **Product Category Name** columna, a continuación, haga clic en **cambiar el nombre de**y, a continuación, escriba `Category`.  
  
    > [!NOTE]  
    >  Al cambiar el nombre de una columna de la jerarquía no se cambia el nombre de esa columna en la tabla. Una columna de una jerarquía es simplemente una representación de la columna de la tabla.  
  
6.  En el `Product` de tabla, haga clic en el **Product Subcategory Name** columna, a continuación, en el menú contextual, elija **agregar a jerarquía**y, a continuación, haga clic en `Category`.  
  
7.  Cambiar el nombre de **nombre de subcategoría de producto** a `Subcategory`.  
  
8.  Mediante el uso de hacer clic y arrastrar o mediante el **agregar a jerarquía** en el menú contextual de comandos, agregue el **nombre del modelo** y **Product Name** columnas (en orden) y colocarlos bajo la **Product Subcategory Name** columna. Cambiar el nombre de estas columnas `Model` y `Product`, respectivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Para crear jerarquías en la tabla Date  
  
1.  En el diseñador de modelos, haga clic con el botón derecho en la tabla **Fecha** y, después, haga clic en **Crear jerarquía**.  
  
2.  Cambie el nombre de la jerarquía a **Calendario**.  
  
3.  Agregue las columnas siguientes, en orden, y después cámbieles el nombre:  
  
    |columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año del calendario|Year|  
    |Semestre del calendario|Semestre|  
    |Trimestre del calendario|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  En la tabla **Fecha** , repita los pasos anteriores y cree una jerarquía **Fiscal** que incluya las siguientes columnas:  
  
    |columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año fiscal|Year|  
    |Semestre fiscal|Semestre|  
    |Trimestre fiscal|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Finalmente, en la tabla **Fecha** , repita los pasos anteriores y cree una jerarquía **Calendario de producción** que incluya las columnas siguientes:  
  
    |columna|Cambiar el nombre a:|  
    |------------|----------------|  
    |Año del calendario|Year|  
    |Week Number Of Year|Semana|  
    |Day Of Week|Day|  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 11: Crear particiones](lesson-10-create-partitions.md).  
  
  