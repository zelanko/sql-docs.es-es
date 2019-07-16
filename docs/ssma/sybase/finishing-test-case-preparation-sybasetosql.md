---
title: Finalización de la preparación del caso de prueba (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3085d17804866015a78e93556dd5373d3a1b8cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029138"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Finalización de la preparación del caso de prueba (SybaseToSQL)
Página final del asistente muestra la descripción del caso de prueba y la información acerca de los objetos que participan en la prueba. Además, en esta página se pueden establecer la prueba de las opciones de ejecución.  
  
El **información del caso de prueba** sección muestra el nombre del caso de prueba y la descripción.  
  
El **objetos de prueba** sección contiene la lista de objetos probados agrupados por tipo de objeto con nombre.  
  
El **objetos afectados se analicen** sección muestra la lista de objetos que se deben comparar los cambios de datos después de la ejecución de objetos probados con nombre.  
  
## <a name="test-case-settings"></a>Configuración de caso de prueba  
En el **configuración de caso de prueba** sección puede establecer la siguiente ejecución de las opciones de prueba:  
  
### <a name="stop-test-execution-after-first-failure"></a>Detener la ejecución de pruebas tras el primer error  
Especifica que la prueba se interrumpe si se produce un error durante la ejecución de pruebas.  
  
-   Si elige **Sí**, interrumpir la ejecución de pruebas si se produce un error.  
  
-   Si elige **No**, continúa la ejecución de pruebas después de un error.  
  
### <a name="perform-data-rollback"></a>Realizar reversión de datos  
Habilitar la reversión automática de los datos después de la ejecución de pruebas.  
  
-   Si elige **Sí**, se perderán los cambios de datos después de la ejecución de pruebas.  
  
-   Si elige **No**, todos los cambios de datos se guardará la ejecución de prueba.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de ahorro de tablas auxiliares  
Define el modo de almacenamiento para las tablas auxiliares creadas durante la ejecución de pruebas. Vea la descripción de las tablas auxiliares en el [ejecutando casos de prueba &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) tema.  
  
-   Si selecciona **guardar siempre**, siempre se almacenarán datos de la tabla auxiliar para su uso posterior.  
  
-   Si selecciona **guardar si la comparación de la tabla no se pudo**, se almacenarán los datos de la tabla auxiliar solo si se produce un error.  
  
-   Si selecciona **eliminar siempre**, tablas auxiliares siempre se elimina después de la ejecución de pruebas.  
  
-   Si selecciona **usuario preguntar si la comparación de la tabla no se pudo**, el usuario puede seleccionar la acción es necesaria si se produce un error.  
  
Haga clic en el **finalizar** botón para guardar el caso de prueba preparados en [utilizando repositorios de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Uso de repositorios de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
