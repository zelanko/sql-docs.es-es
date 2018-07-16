---
title: 'Lección 3: Buscar datos coincidentes para quitar duplicados de lista de proveedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f244dc7d62f19967aae7ee3bc32a634008fcc94e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265797"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>Lección 3: buscar datos coincidentes para quitar duplicados de lista de proveedores
  Para preparar la base de conocimiento que se va a usar para realizar la actividad de coincidencia, hay que crear una directiva de coincidencia en la base de conocimiento. Solo puede haber una directiva de coincidencia en una base de conocimiento. Una directiva de coincidencia se compone de una o más reglas de coincidencia. Una regla identifica los dominios implicados en el proceso de coincidencia y especifica el peso que tiene cada valor de dominio sobre en el criterio de coincidencia. En la regla se debe especificar si los valores de dominio deben ser una coincidencia exacta o pueden ser similares, y hasta qué punto. También se especifica si una coincidencia de dominio es un requisito previo para el proceso de coincidencia. Puede probar cada regla por separado y probar toda la directiva con datos de ejemplo. El proceso de pruebas muestra los registros cuyas puntuaciones de coincidencia son mayores que el **puntuación de registro mínima** umbral especificado en la configuración de DQS en un clúster (grupo). Puede seguir modificando las reglas de la directiva hasta que esté satisfecho con los resultados.  
  
 Después de definir la directiva, creará un proyecto de calidad de los datos para ejecutar la actividad de coincidencia. El proyecto de búsqueda de coincidencias aplica las reglas de coincidencia de la directiva correspondiente al origen de datos que se va a evaluar. Este proceso evalúa la probabilidad de que dos filas cualesquiera sean coincidencias. Cuando DQS realiza el análisis de coincidencia, crea clústeres de registros que considera como coincidencias. DQS identifica de forma aleatoria uno de los registros como registro dinámico. Puede comprobar y rechazar los registros que no sean una coincidencia adecuada para el clúster. Consulte [crear una directiva de coincidencia](http://msdn.microsoft.com/library/hh270290.aspx) tema para obtener más detalles.  
  
 En esta lección, realizará una actividad de coincidencia para quitar duplicados de la lista de proveedores. Primero creará una directiva de coincidencia con una regla para identificar los duplicados de la lista de proveedores y publicará la directiva en la base de conocimiento. Después, creará y ejecutará un proyecto de calidad de datos para buscar coincidencias. Por último, exportará los resultados de la actividad de coincidencia a un archivo de Excel que usará más adelante para cargar datos en Master Data Services (MDS).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 1: Definir una directiva de coincidencia](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
