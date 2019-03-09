---
title: 'Analysis Services tutorial lección 8: creación de perspectivas | Microsoft Docs'
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
ms.openlocfilehash: 29a49478d75d7af5670f3e693cd87a5238c4ae11
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57684942"
---
# <a name="create-perspectives"></a>Crear perspectivas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará una perspectiva venta por Internet. Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación. Cuando un usuario se conecta a un modelo mediante una perspectiva, verán sólo los objetos de modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva. Para obtener más información, consulte [Perspectivas](../tabular-models/perspectives-ssas-tabular.md).
  
La perspectiva de ventas por Internet que creará en esta lección excluye el objeto de tabla DimCustomer. Cuando se crea una perspectiva que excluye ciertos objetos de vista, ese objeto todavía existe en el modelo. Sin embargo, no está visible en una lista de campos de cliente de informes. Las columnas calculadas y medidas se pueden incluir en una perspectiva o no pueden calcularse a partir de los datos del objeto excluido.  
  
El propósito de esta lección es describir cómo se crean las perspectivas y permitir que se familiarice con las herramientas de creación de modelos tabulares. Si posteriormente amplía este modelo para incluir tablas adicionales, puede crear otras perspectivas para definir puntos de vista diferentes del modelo, por ejemplo, inventario y ventas.  
  
Tiempo estimado para completar esta lección: **Cinco minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 7: Creación de indicadores clave de rendimiento](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Crear perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para crear una perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú > **perspectivas** > **crear y administrar**.  
  
2.  En el cuadro de diálogo **Perspectivas** , haga clic en **Nueva perspectiva**.  
  
3.  Haga doble clic en el **nueva perspectiva** encabezado de columna y, a continuación, cambie el nombre **Internet Sales**.  
  
4.  Seleccionar todas las tablas *excepto* **DimCustomer**.  
  
    ![perspectivas como lección 8](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    En una lección posterior, utilice la analizar en función de Excel para probar esta perspectiva. La lista de campos de tabla dinámica de Excel incluye todas las tablas, excepto dimcustomer.  

## <a name="whats-next"></a>¿Qué sigue?

[Lección 9: Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).
  
  
  
  
