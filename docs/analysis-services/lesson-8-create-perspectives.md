---
title: "Lección 9 crear perspectivas | Documentos de Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 993cf02a47240c0a74667f6220c6b2dd5d6df86c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-8-create-perspectives"></a>Lección 8: Crear perspectivas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, creará una perspectiva Venta por Internet. Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación. Cuando un usuario se conecta a un modelo mediante una perspectiva, podrán ver sólo los objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva.  
  
La perspectiva de ventas por Internet que cree en esta lección excluirá el objeto de la tabla DimCustomer. Al crear una perspectiva que excluye ciertos objetos en la vista, ese objeto todavía existe en el modelo; sin embargo, no está visible en una lista de campos del cliente de informe. Las columnas calculadas y medidas se pueden incluir en una perspectiva o no pueden calcularse a partir de los datos del objeto excluido.  
  
El propósito de esta lección es describir cómo se crean las perspectivas y permitir que se familiarice con las herramientas de creación de modelos tabulares. Si posteriormente amplía el modelo para incluir tablas adicionales, puede crear otras perspectivas para definir puntos de vista diferentes del modelo, por ejemplo, inventario y las ventas. Para obtener más información, consulte [Perspectivas](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 7: crear indicadores clave de rendimiento](../analysis-services/lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Crear perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para crear una perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú > **perspectivas** > **crear y administrar**.  
  
2.  En el cuadro de diálogo **Perspectivas** , haga clic en **Nueva perspectiva**.  
  
3.  Haga doble clic en el **nueva perspectiva** encabezado de columna y, a continuación, cambie el nombre **venta por Internet**.  
  
4.  Seleccione todas las tablas *excepto* **DimCustomer**.  
  
    ![como-tabular-lección 8-perspectivas](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    En una lección posterior, utilizará la analizar en función de Excel para probar esta perspectiva. La lista de campos de tabla dinámica de Excel incluirá cada tabla excepto la tabla DimCustomer.  

## <a name="whats-next"></a>¿Qué debe hacer a continuación?
Vaya a la siguiente lección: [lección 9: crear jerarquías](../analysis-services/lesson-9-create-hierarchies.md).
  
  
  
  

