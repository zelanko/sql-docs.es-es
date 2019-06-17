---
title: Uso de repositorios de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cae34190da8179663996c7a385cc13541353ee0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283522"
---
# <a name="using-test-repositories-oracletosql"></a>Uso de repositorios de prueba (OracleToSQL)
Los almacenes de repositorio de pruebas de SSMA SSMA evaluador casos de prueba y los resultados de pruebas para su uso posterior. Los datos del repositorio se guardan en las tablas de SQL Server **TestCaseRepository** y **RunTestCaseResultRepository** en el esquema **ssma_oracle_utilities** de **ssmatesterdb** base de datos.  
  
Los siguientes botones están disponibles en el cuadro de diálogo de repositorio de los casos de prueba:  
  
-   Haga clic en el **actualizar** botón para actualizar la lista de casos de prueba o los resultados de pruebas.  
  
-   Haga clic en el **cerrar** botón para cerrar el cuadro de diálogo de repositorio de los casos de prueba.  
  
## <a name="test-cases-repository"></a>Repositorio de casos de prueba  
Puede ver el repositorio de los casos de prueba haciendo **casos de prueba...**  desde el **evaluador** menú. SSMA, a continuación, muestra el **repositorio de los casos de prueba** ventana de cuadro de diálogo con una lista de casos de prueba guardadas en el **casos de prueba** página.  
  
La cuadrícula muestra la siguiente información sobre cada caso de prueba:  
  
-   Nombre: El nombre del caso de prueba.  
  
-   Creado: La fecha de creación de casos de prueba.  
  
-   Puede modificar: La fecha de última modificación del caso de prueba.  
  
-   Descripción: Las descripciones del caso de prueba.  
  
Los siguientes botones están disponibles en la página de casos de prueba:  
  
-   Haga clic en el **agregar** botón para ejecutar el Asistente de caso de prueba y crear una nueva prueba.  
  
-   Haga clic en el **quitar** botón para eliminar la prueba seleccionada desde el repositorio. Cuando se elimina un caso de prueba, también se eliminan todos los resultados de pruebas relacionados.  
  
-   Haga clic en el **editar** botón para ejecutar el Asistente de caso de prueba y cambiar la prueba seleccionada.  
  
-   Haga clic en el **ejecutar** botón para abrir el [ejecutando casos de prueba (OracleToSQL)](https://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) cuadro de diálogo y ejecutar la prueba seleccionada.  
  
## <a name="test-results-repository"></a>Repositorio de resultados de pruebas  
Puede ver el repositorio de resultados de pruebas en el **los resultados de pruebas** página de la **repositorio de los casos de prueba** ventana. Haga clic en **los resultados de pruebas...**  desde el **evaluador** menú.  
  
Puede usar dos filtros en **los resultados de pruebas** página:  
  
-   El filtro de nombre de caso de prueba: Permite elegir los resultados de pruebas por el nombre del caso de prueba. Este filtro **todos los casos de prueba** valor permite mostrar los resultados de pruebas para todos los casos de prueba.  
  
-   El filtro de fecha de ejecución de casos de prueba: Filtros de resultados de pruebas por la fecha de guardar. Este filtro **período todas** valor permite mostrar los resultados de pruebas para cualquier fecha de guardar.  
  
La siguiente información sobre los resultados de pruebas se muestra en la cuadrícula.  
  
-   Nombre: Nombre del caso de prueba.  
  
-   Guardado: Fecha del caso de prueba de guardar.  
  
-   Resultados: Un breve resumen de ejecución de pruebas (información sobre herramientas de la celda muestra un resumen completo de la ejecución de pruebas).  
  
Los siguientes botones están disponibles en la página de resultados de pruebas:  
  
-   Haga clic en el **vista** botón para abrir [ver informes de casos de prueba &#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) de resultado de caso de prueba actual.  
  
-   Haga clic en el **eliminar** botón para eliminar el resultado de la prueba seleccionada  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
