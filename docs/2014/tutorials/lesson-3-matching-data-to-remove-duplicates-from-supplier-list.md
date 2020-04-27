---
title: 'Lección 3: datos coincidentes para quitar duplicados de la lista de proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c59a2fce106b08f53722ce44ae69225b680d7925
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484653"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>Lección 3: Búsqueda de datos coincidentes para quitar duplicados de lista de proveedores
  Para preparar la base de conocimiento que se va a usar para realizar la actividad de coincidencia, hay que crear una directiva de coincidencia en la base de conocimiento. Solo puede haber una directiva de coincidencia en una base de conocimiento. Una directiva de coincidencia se compone de una o más reglas de coincidencia. Una regla identifica los dominios implicados en el proceso de coincidencia y especifica el peso que tiene cada valor de dominio sobre en el criterio de coincidencia. En la regla se debe especificar si los valores de dominio deben ser una coincidencia exacta o pueden ser similares, y hasta qué punto. También se especifica si una coincidencia de dominio es un requisito previo para el proceso de coincidencia. Puede probar cada regla por separado y probar toda la directiva con datos de ejemplo. El proceso de prueba muestra los registros cuyas puntuaciones de coincidencia son mayores que el umbral de **puntuación de registro mínimo** especificado en la configuración de DQS en un clúster (grupo). Puede seguir modificando las reglas de la directiva hasta que esté satisfecho con los resultados.  
  
 Después de definir la directiva, creará un proyecto de calidad de los datos para ejecutar la actividad de coincidencia. El proyecto de búsqueda de coincidencias aplica las reglas de coincidencia de la directiva correspondiente al origen de datos que se va a evaluar. Este proceso evalúa la probabilidad de que dos filas cualesquiera sean coincidencias. Cuando DQS realiza el análisis de coincidencia, crea clústeres de registros que considera como coincidencias. DQS identifica de forma aleatoria uno de los registros como registro dinámico. Puede comprobar y rechazar los registros que no sean una coincidencia adecuada para el clúster. Consulte [el tema crear una directiva de coincidencia](https://msdn.microsoft.com/library/hh270290.aspx) para obtener más detalles.  
  
 En esta lección, realizará una actividad de coincidencia para quitar duplicados de la lista de proveedores. Primero creará una directiva de coincidencia con una regla para identificar los duplicados de la lista de proveedores y publicará la directiva en la base de conocimiento. Después, creará y ejecutará un proyecto de calidad de datos para buscar coincidencias. Por último, exportará los resultados de la actividad de coincidencia a un archivo de Excel que usará más adelante para cargar datos en Master Data Services (MDS).  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 1: Definición de una directiva de coincidencia](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
