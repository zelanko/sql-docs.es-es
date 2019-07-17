---
title: Crear una relación en modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e9ee96a04aa6b023be51f8e1e8d913e26a7e2a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207737"
---
# <a name="create-a-relationship"></a>Crear una relación 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Si entre las tablas del origen de datos no hay relaciones existentes, o si agrega nuevas tablas, puede usar las herramientas del diseñador de modelos para crear relaciones. Para obtener información acerca de cómo se usan las relaciones en los modelos tabulares, vea [relaciones](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="create-a-relationship-between-two-tables"></a>Crear una relación entre dos tablas  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>Para crear una relación entre dos tablas en la Vista de diagrama (hacer clic y arrastrar)  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** , a continuación, en **Vista de modelo**y, por último, en **Vista de diagrama**.  
  
2.  Haga clic (y mantenga presionado el botón) en una columna de una tabla, a continuación arrastre el cursor a una columna de búsqueda relacionada en una tabla de búsqueda relacionada y suelte el botón. La relación se creará automáticamente en el orden correcto.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>Para crear una relación entre dos tablas en la Vista de diagrama (hacer clic con el botón secundario)  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** , a continuación, en **Vista de modelo**y, por último, en **Vista de diagrama**.  
  
2.  Haga clic con el botón derecho en el encabezado de una tabla o en una columna y, luego, haga clic en **Crear relación**.  
  
3.  En el cuadro de diálogo **Crear relación** , haga clic en la flecha abajo de **Tabla**y seleccione una tabla en la lista desplegable.  
  
     En una relación de uno a varios, esta tabla debe estar en el extremo de "varios".  
  
4.  En **Columna**, seleccione la columna que contiene los datos que se relacionan con **Columna de búsqueda relacionada**. La columna se selecciona automáticamente si hizo clic con el botón secundario en una columna para crear la relación.  
  
5.  En **Columna de búsqueda relacionada**, seleccione una tabla que tenga al menos una columna de datos relacionada con la tabla que acaba de seleccionar en **Tabla**.  
  
     En una relación "uno a varios", esta tabla debería estar en el extremo "uno", lo que quiere decir que los valores de la columna seleccionada no contienen duplicados. Si intenta crear la relación en el orden equivocado (uno a varios en lugar de varios a uno), se mostrará un icono al lado del campo **Columna de búsqueda relacionada** . Invierta el orden para crear una relación válida.  
  
6.  En **Columna de búsqueda relacionada**, seleccione una columna que tenga valores únicos que coincidan con los valores seleccionados para **Columna**.  
  
7.  Haga clic en **Create**(Crear).  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>Para crear una relación entre dos tablas en la vista de datos  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Tabla** y, a continuación, en **Crear relaciones**.  
  
2.  En el cuadro de diálogo **Crear relación** , haga clic en la flecha abajo de **Tabla**y seleccione una tabla en la lista desplegable.  
  
     En una relación de uno a varios, esta tabla debe estar en el extremo de "varios".  
  
3.  En **Columna**, seleccione la columna que contiene los datos que se relacionan con **Columna de búsqueda relacionada**.  
  
4.  En **Columna de búsqueda relacionada**, seleccione una tabla que tenga al menos una columna de datos relacionada con la tabla que acaba de seleccionar en **Tabla**.  
  
     En una relación "uno a varios", esta tabla debería estar en el extremo "uno", lo que quiere decir que los valores de la columna seleccionada no contienen duplicados. Si intenta crear la relación en el orden equivocado (uno a varios en lugar de varios a uno), se mostrará un icono al lado del campo **Columna de búsqueda relacionada** . Invierta el orden para crear una relación válida.  
  
5.  En **Columna de búsqueda relacionada**, seleccione una columna que tenga valores únicos que coincidan con los valores seleccionados para **Columna**.  
  
6.  Haga clic en **Create**(Crear).  
  
## <a name="see-also"></a>Vea también  
 [Eliminar relaciones](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [Relaciones](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  
