---
title: Finalizar la preparación del caso de prueba (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
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
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cf1519483abcf25493e036bc524c6fdc9a1e919e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Finalizar la preparación del caso de prueba (SybaseToSQL)
Página final del asistente muestra la descripción del caso de prueba y obtener información acerca de los objetos implicados en la prueba. Además, en esta página se pueden establecer la prueba de opciones de ejecución.  
  
El **información casos de prueba** sección muestra el nombre del caso de prueba y la descripción.  
  
El **objetos de prueba** sección contiene la lista con nombre de objetos probados agrupados por tipo de objeto.  
  
El **objetos afectados que analizarse** sección muestra la lista de objetos que se deben comparar los cambios de datos después de la ejecución de objetos probados con nombre.  
  
## <a name="test-case-settings"></a>Configuración de caso de prueba  
En el **configuración de caso de prueba** sección puede establecer la siguiente ejecución de opciones de prueba:  
  
### <a name="stop-test-execution-after-first-failure"></a>Detener la ejecución de prueba tras el primer error  
Especifica que la prueba se interrumpe si se produce un error durante la ejecución de prueba.  
  
-   Si elige **Sí**, interrumpir la ejecución de pruebas si se produce un error.  
  
-   Si elige **n**, continúa la ejecución de pruebas después de un error.  
  
### <a name="perform-data-rollback"></a>Realizar la reversión de datos  
Habilitar la reversión automática de los datos después de la ejecución de prueba.  
  
-   Si elige **Sí**, se perderán los cambios de datos después de la ejecución de prueba.  
  
-   Si elige **n**, todos los cambios de datos se guardarán de ejecución de prueba.  
  
### <a name="auxiliary-tables-saving-mode"></a>Tablas auxiliares de modo de ahorro  
Define el modo de guardar para tablas auxiliares creados durante la ejecución de pruebas. Vea la descripción de las tablas auxiliares en el [ejecutar casos de prueba &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) tema.  
  
-   Si selecciona **guardar siempre**, siempre se almacenarán datos de la tabla auxiliar para su uso posterior.  
  
-   Si selecciona **guardar si la comparación de la tabla no se pudo**, se almacenarán los datos de la tabla auxiliar solo si se produce un error.  
  
-   Si selecciona **siempre eliminar**, siempre puede eliminar tablas auxiliares después de la ejecución de prueba.  
  
-   Si selecciona **preguntar al usuario si la comparación de la tabla no se pudo**, el usuario puede seleccionar la acción es necesaria si se produce un error.  
  
Haga clic en el **finalizar** botón para guardar el caso de prueba preparada en [repositorios de prueba usando &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Uso de repositorios de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas de objetos de base de datos migran &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
