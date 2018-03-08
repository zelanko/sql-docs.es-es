---
title: "Lección de Analysis Services tutorial 3: marcar como tabla de fechas | Documentos de Microsoft"
description: "Describe cómo marcar una tabla de fechas en el proyecto de tutorial de Analysis Services."
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: b747791b4e33683c2eaad73b3d19d80e7c10f601
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="mark-as-date-table"></a>Marcar como tabla de fechas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En la lección 2: Obtener datos, importó una tabla de dimensiones denominada **DimDate**. Mientras que en el modelo de esta tabla se denomina DimDate, también se conoce como un *tabla de fechas*, ya que contiene datos de fecha y hora.  
  
Siempre que use las funciones de inteligencia de tiempo DAX, como cuando crea las medidas más adelante, deberá especificar las propiedades que incluyen un *tabla de fechas* y un identificador único *columna de fecha* de esa tabla.
  
En esta lección, marcar la **DimDate** tabla como el *tabla de fechas* y **fecha** columna (en la tabla Date) como el *columna de fecha* (único identificador).  

Para marcar la tabla de fechas y la columna de fecha, es un buen momento para realizar el mantenimiento de manera un poco para que sea más fácil entender el modelo. Observe que en la tabla DimDate una columna denominada **FullDateAlternateKey**. Esta columna contiene una fila por cada día de cada año de calendario incluido en la tabla. Utilice esta columna mucho en fórmulas de medida y en los informes. Sin embargo, FullDateAlternateKey no es realmente un buen identificador para esta columna. Cambiar el nombre a **fecha**, lo que sea más fácil identificar e incluir en las fórmulas. Siempre que sea posible, es una buena idea cambiar el nombre de objetos, como tablas y columnas para que sean fáciles de identificar en SSDT y las aplicaciones de informes. 
  
Tiempo estimado para completar esta lección: **tres minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 2: obtener datos](../tutorial-tabular-1400/as-lesson-2-get-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para cambiar el nombre de la columna FullDateAlternateKey

1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.

2.  Haga doble clic en el encabezado de la **FullDateAlternateKey** columna y, a continuación, cambie su nombre a **fecha**.

  
### <a name="to-set-mark-as-date-table"></a>Para establecer la marca como tabla de fecha  
  
1.  Seleccione la columna **Date** y, en la ventana **Propiedades** , en **Tipo de datos**, asegúrese de que  **Date** está seleccionada.  
  
2.  Haga clic en el menú **Tabla** , haga clic en **Date**y, después, haga clic en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date** , seleccione la columna **Date** como identificador único. Normalmente se selecciona de forma predeterminada. Haga clic en **Aceptar**. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>¿Qué sigue?

[Lección 4: Crear relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md).
  
