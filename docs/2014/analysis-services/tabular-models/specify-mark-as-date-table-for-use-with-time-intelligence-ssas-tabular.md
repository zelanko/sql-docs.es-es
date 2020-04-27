---
title: Especificar marcar como tabla de fechas para su uso con inteligencia de tiempo (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27a03aaf94d518caa6b649b7ccd826e08798dacb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284883"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a>Especificar Marcar como tabla de fechas con inteligencia de tiempo (SSAS tabular)
  Para usar las funciones de inteligencia de tiempo en fórmulas DAX, debe especificar una tabla de fechas y una columna de identificador único (datetime) del tipo de datos Date. Una vez especificada una columna en la tabla de fechas como identificador único, puede crear relaciones entre las columnas de la tabla de fechas y cualquier tabla de hechos.  
  
 Cuando se usan las funciones de inteligencia de tiempo, se aplican las siguientes reglas:  
  
-   Cuando use funciones de inteligencia de tiempo DAX, no especifique nunca una columna datetime desde una tabla de hechos. Cree siempre una tabla de fechas independiente en el modelo con al menos una columna datetime del tipo de datos Date y con valores únicos.  
  
-   Asegúrese de que la tabla de fechas tiene un intervalo de fechas continuo.  
  
-   La columna datetime de la tabla de fechas debe estar desglosada por día (sin fracciones de día).  
  
-   Debe especificar una tabla de fechas y una columna de identificador único mediante el cuadro de diálogo **Marcar como tabla de fechas** .  
  
-   Cree relaciones entre las tablas de hechos y las columnas de tipo de datos Date en la tabla de fechas.  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>Para especificar una tabla de fechas y un identificador único  
  
1.  En el diseñador de modelos, haga clic en la tabla de fechas.  
  
2.  Haga clic en el menú **Tabla** , haga clic en **Fecha**y después haga clic en **Marcar como tabla de fechas**  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** , en el cuadro de lista **Fecha** , seleccione la columna que se utilizará como identificador único. Esta columna debe contener valores únicos y debe ser de tipo de datos Date. Por ejemplo:  
  
    |Fecha|  
    |----------|  
    |1/7/2010 12:00:00 a.m.|  
    |2/7/2010 12:00:00 a.m.|  
    |3/7/2010 12:00:00 a.m.|  
    |4/7/2010 12:00:00 a.m.|  
    |5/7/2010 12:00:00 a.m.|  
  
4.  Si fuera necesario, cree las relaciones entre las tablas de hechos y la tabla de fechas.  
  
## <a name="see-also"></a>Consulte también  
 [Cálculos &#40;&#41;tabular de SSAS](calculations-ssas-tabular.md)   
 [Funciones de inteligencia de tiempo &#40;DAX&#41;](/dax/time-intelligence-functions-dax)  
  
  
