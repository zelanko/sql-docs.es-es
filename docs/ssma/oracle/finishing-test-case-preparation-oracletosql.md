---
title: Finalización de la preparación del caso de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1bdbe8616f5f2c3252f813e6e2636966ff16ec16
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51662284"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>Finalización de la preparación del caso de prueba (OracleToSQL)
Página final del asistente muestra la descripción del caso de prueba y la información acerca de los objetos que participan en la prueba. Además, en esta página se pueden establecer la prueba de las opciones de ejecución.  
  
El **información del caso de prueba** sección muestra el nombre del caso de prueba y la descripción.  
  
El **objetos seleccionados para ser probado** sección contiene la lista de objetos probados agrupados por tipo de objeto con nombre.  
  
El **objetos afectados por prueba que se va a analizar** sección muestra la lista de objetos que se deben comparar los cambios de datos después de la ejecución de objetos probados con nombre.  
  
## <a name="test-case-settings"></a>Configuración de caso de prueba  
En el **configuración de caso de prueba** sección puede establecer la siguiente ejecución de las opciones de prueba:  
  
### <a name="stop-test-execution-after-first-failure"></a>Detener la ejecución de pruebas tras el primer error  
Especifica que la prueba se interrumpe si se produce un error durante la ejecución de pruebas.  
  
-   Si elige **Sí**, interrumpir la ejecución de pruebas si se produce un error.  
  
-   Si elige **No**, continúa la ejecución de pruebas después de un error.  
  
### <a name="perform-data-rollback"></a>Realizar reversión de datos  
Permite la reversión automática de los datos después de la ejecución de pruebas.  
  
-   Si elige **Sí**, se perderán los cambios de datos después de la ejecución de pruebas.  
  
-   Si elige **No**, todos los cambios de datos se guardará la ejecución de prueba.  
  
### <a name="auxiliary-tables-saving-mode"></a>Modo de ahorro de tablas auxiliares  
Define el modo de almacenamiento para las tablas auxiliares creadas durante la ejecución de pruebas. Vea la descripción de las tablas auxiliares en el [ejecutando casos de prueba &#40;OracleToSQL&#41; ](../../ssma/oracle/running-test-cases-oracletosql.md) tema.  
  
-   Si selecciona **guardar siempre**, siempre se almacenarán datos de la tabla auxiliar para su uso posterior.  
  
-   Si selecciona **guardar si la comparación de la tabla no se pudo**, se almacenarán los datos de la tabla auxiliar solo si se produce un error.  
  
-   Si selecciona **eliminar siempre**, tablas auxiliares siempre se elimina después de la ejecución de pruebas.  
  
-   Si selecciona **usuario preguntar si la comparación de la tabla no se pudo**, el usuario puede seleccionar la acción es necesaria si se produce un error.  
  
Haga clic en el **finalizar** botón para guardar el caso de prueba preparados en [utilizando repositorios de prueba (OracleToSQL)](https://msdn.microsoft.com/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Vea también  
[Uso de repositorios de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Ejecutar casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
