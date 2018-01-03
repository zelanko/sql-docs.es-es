---
title: Ver informes de casos de prueba (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: ea0d497348f6fb146f5633d561385f44816a8871
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="viewing-test-case-reports-oracletosql"></a>Ver informes de casos de prueba (OracleToSQL)
El informe de casos de prueba muestra los resultados de pruebas de comprobación y la información de prueba general. En caso de error de prueba, también se muestra información sobre los datos que no coincidan en objetos comprobados.  
  
## <a name="report-structure"></a>Estructura de informe  
La parte superior del informe muestra estas estadísticas:  
  
-   El número total de objetos probados y el número de objetos para el que la prueba fue correcta.  
  
-   El número total de tablas comprobadas y claves externas y el número de tablas y claves externas coincidentes correctamente.  
  
-   La hora de inicio, hora de finalización del caso de prueba y el tiempo total empleado para la ejecución.  
  
El resto del informe muestra información en cuatro categorías:  
  
**Errores de requisitos previos**  
Muestra los errores producidos en el **paso de requisitos previos.** Normalmente, se omite.  
  
**Inicialización**  
Muestra el estado de ejecución como **correcto** o **error**.  
  
**Resultado de prueba de objetos**  
Una comparación de los resultados (éxito o error) y las diferencias que SSMA evaluador detectó en caso de error.  
  
**Finalización**  
Muestra el estado de ejecución como **correcto** o **error**.  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas migran objetos de base de datos &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
