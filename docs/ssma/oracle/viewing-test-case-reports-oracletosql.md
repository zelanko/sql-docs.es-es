---
title: Visualización de informes de casos de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ce59e126ce24e30e091b4a5456d8b78c84355e88
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641774"
---
# <a name="viewing-test-case-reports-oracletosql"></a>Visualización de informes de casos de prueba (OracleToSQL)
El informe de casos de prueba muestra los resultados de la prueba comprobación y la información de prueba general. En caso de error de prueba, también se muestra información acerca de los datos que no coincidentes en objetos comprobados.  
  
## <a name="report-structure"></a>Estructura de informe  
La parte superior del informe muestra estas estadísticas:  
  
-   El número total de objetos probados y el número de objetos para el que la prueba fue correcta.  
  
-   El número total de tablas comprobadas y claves externas y el número de tablas y claves externas coinciden correctamente.  
  
-   La hora de inicio, hora de finalización del caso de prueba y el tiempo total necesario para la ejecución.  
  
El resto del informe muestra información en cuatro categorías:  
  
**Errores de requisitos previos**  
Muestra los errores producidos en el **paso de requisitos previos.** Normalmente, se omite.  
  
**Inicialización**  
Muestra el estado de ejecución como **éxito** o **error**.  
  
**Resultado de los objetos de la prueba**  
Comparación de los resultados (éxito o error) y las diferencias de SSMA evaluador detectado en caso de error.  
  
**Finalización**  
Muestra el estado de ejecución como **éxito** o **error**.  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
