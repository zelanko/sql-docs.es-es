---
title: Análisis de 8 crear las perspectivas de lecciones del tutorial de servicios | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6de14f79ab00f489913153abefa1ae40aa5608e7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-perspectives"></a>Crear perspectivas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará una perspectiva venta por Internet. Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación. Cuando un usuario se conecta a un modelo mediante una perspectiva, podrán ver sólo los objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva. Para obtener más información, consulte [perspectivas](../tabular-models/perspectives-ssas-tabular.md).
  
La perspectiva de ventas por Internet que cree en esta lección excluye el objeto de la tabla DimCustomer. Cuando se crea una perspectiva que excluye ciertos objetos de vista, ese objeto sigue existiendo en el modelo. Sin embargo, no está visible en una lista de campos de cliente de informes. Las columnas calculadas y medidas se pueden incluir en una perspectiva o no pueden calcularse a partir de los datos del objeto excluido.  
  
El propósito de esta lección es describir cómo se crean las perspectivas y permitir que se familiarice con las herramientas de creación de modelos tabulares. Si posteriormente amplía el modelo para incluir tablas adicionales, puede crear otras perspectivas para definir puntos de vista diferentes del modelo, por ejemplo, inventario y las ventas.  
  
Tiempo estimado para completar esta lección: **cinco minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 7: crear indicadores clave de rendimiento](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Crear perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para crear una perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú > **perspectivas** > **crear y administrar**.  
  
2.  En el cuadro de diálogo **Perspectivas** , haga clic en **Nueva perspectiva**.  
  
3.  Haga doble clic en el **nueva perspectiva** encabezado de columna y, a continuación, cambie el nombre **venta por Internet**.  
  
4.  Seleccione todas las tablas *excepto* **DimCustomer**.  
  
    ![perspectivas como lección 8](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    En una lección posterior, usa la característica analizar en Excel para probar esta perspectiva. La lista de campos de tabla dinámica de Excel incluye cada tabla excepto la tabla DimCustomer.  

## <a name="whats-next"></a>¿Qué sigue?

[Lección 9: Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).
  
  
  
  
