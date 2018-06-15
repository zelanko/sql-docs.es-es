---
title: Lección 9 crear perspectivas | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e917e817768571e1959ae6163743ecdad0409af
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019792"
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

## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 9: crear jerarquías](../analysis-services/lesson-9-create-hierarchies.md).
  
  
  
  
