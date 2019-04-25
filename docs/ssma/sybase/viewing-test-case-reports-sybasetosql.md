---
title: Visualización de informes de casos de prueba (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 840f73d0732d0789d378c6f1bceb100c58e01bb6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625849"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Visualización de informes de casos de prueba (SybaseToSQL)
El informe de casos de prueba muestra los resultados de la prueba comprobación y la información de prueba general. En caso de error de prueba, también se muestra información acerca de los datos que no coincidentes en objetos comprobados.  
  
## <a name="report-structure"></a>Estructura de informe  
La parte superior del informe muestra estas estadísticas:  
  
-   El número total de objetos probados y el número de objetos para el que la prueba fue correcta.  
  
-   El número total de tablas comprobadas y claves externas y el número de tablas y claves externas coinciden correctamente.  
  
-   La hora de inicio, hora de finalización del caso de prueba y el tiempo total necesario para la ejecución.  
  
El resto del informe muestra información en cuatro categorías:  
  
**Errores de requisitos previos**  
Muestra los errores producidos en el **requisitos previos** paso. Normalmente, se omite.  
  
**Inicialización**  
Muestra el estado de ejecución como **éxito** o **error**.  
  
**Resultado de los objetos de la prueba**  
Comparación de los resultados (éxito o error) y las diferencias de SSMA evaluador detectado en caso de error.  
  
**Finalización**  
Muestra el estado de ejecución como **éxito** o **error**.  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
