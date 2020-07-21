---
title: 'Tarea 3: limpiar datos con la base de conocimiento proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 647c924a-9b91-4294-8d96-e81416e4e90e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 13201a8b904a5fc5232b9fa860710e4e39cce67a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064760"
---
# <a name="task-3-cleansing-data-against-the-suppliers-knowledge-base"></a>Tarea 3: Limpieza de datos en la base de conocimiento Proveedores
  En esta tarea, ejecutará el proceso de limpieza asistida por PC. DQS emplea algoritmos avanzados y niveles de confianza basados en los valores de umbral especificados para analizar los datos comparándolos con la base de conocimiento seleccionada; a continuación, los limpia. Vea [Limpiar datos mediante el conocimiento de DQS (interno)](https://msdn.microsoft.com/library/hh213061.aspx) para obtener más detalles.

1.  Haga clic en **Iniciar** para iniciar el proceso de limpieza asistido por PC.

     ![Página de limpieza del proceso de limpieza](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-01.jpg "Página de limpieza del proceso de limpieza")

2.  Una vez completado el proceso de limpieza, revise las **estadísticas** en la pestaña **generador de perfiles** . Las estadísticas de origen proporcionan el número de registros procesados, el número de registros que se detectan como correctos, el número de registros que DQS corrige, el número de registros que tienen cambios sugeridos por DQS y el número de registros que no son válidos. En el cuadro de lista de la derecha puede ver los valores corregidos, los valores sugeridos y la integridad (la medida en la que los datos están presentes) y la precisión (la medida en que los datos se pueden usar para los fines previstos) de los valores de todos los dominios implicados en el proceso de limpieza.

     ![Resultados de la limpieza](../../2014/tutorials/media/et-cleansingdataagainstthesupplierkb-02.jpg "Resultados de la limpieza")

3.  Haga clic en **Siguiente** para cambiar a la página **Administrar y ver resultados** .

## <a name="next-step"></a>siguiente paso
 [Tarea 4: administrar y ver los resultados](../../2014/tutorials/task-4-manaing-and-viewing-results.md)


