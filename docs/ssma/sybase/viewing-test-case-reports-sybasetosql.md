---
title: Ver informes de casos de prueba (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 69321fdc62eb87b35f183e87ab49a46c3fbb6b21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Ver informes de casos de prueba (SybaseToSQL)
El informe de casos de prueba muestra los resultados de pruebas de comprobación y la información de prueba general. En caso de error de prueba, también se muestra información sobre los datos que no coincidan en objetos comprobados.  
  
## <a name="report-structure"></a>Estructura de informe  
La parte superior del informe muestra estas estadísticas:  
  
-   El número total de objetos probados y el número de objetos para el que la prueba fue correcta.  
  
-   El número total de tablas comprobadas y claves externas y el número de tablas y claves externas coincidentes correctamente.  
  
-   La hora de inicio, hora de finalización del caso de prueba y el tiempo total empleado para la ejecución.  
  
El resto del informe muestra información en cuatro categorías:  
  
**Errores de requisitos previos**  
Muestra los errores producidos en el **requisitos previos** paso. Normalmente, se omite.  
  
**Inicialización**  
Muestra el estado de ejecución como **correcto** o **error**.  
  
**Resultado de prueba de objetos**  
Una comparación de los resultados (éxito o error) y las diferencias que SSMA evaluador detectó en caso de error.  
  
**Finalización**  
Muestra el estado de ejecución como **correcto** o **error**.  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas de objetos de base de datos migran &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
