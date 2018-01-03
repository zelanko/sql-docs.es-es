---
title: Uso de repositorios de prueba (OracleToSQL) | Documentos de Microsoft
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
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 4412d7de5cd86071f2d1c25354e85266f33bccc7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-test-repositories-oracletosql"></a>Uso de repositorios de prueba (OracleToSQL)
Los almacenes de repositorio de pruebas de SSMA SSMA evaluador casos de prueba y los resultados de pruebas para su uso posterior. Los datos del repositorio se guardan en las tablas de SQL Server **TestCaseRepository** y **RunTestCaseResultRepository** en el esquema **ssma_oracle_utilities** de **ssmatesterdb** base de datos.  
  
Los siguientes botones están disponibles en el cuadro de diálogo de repositorio de los casos de prueba:  
  
-   Haga clic en el **actualizar** botón para actualizar la lista de casos de prueba o los resultados de pruebas.  
  
-   Haga clic en el **cerrar** botón para cerrar el cuadro de diálogo de repositorio de los casos de prueba.  
  
## <a name="test-cases-repository"></a>Repositorio de casos de prueba  
Puede ver el repositorio de casos de prueba, haga clic en **casos de prueba...** desde el **Tester** menú. SSMA, a continuación, muestra la **repositorio de casos de prueba** ventana de cuadro de diálogo con una lista de los casos de prueba guardados en el **casos de prueba** página.  
  
La cuadrícula muestra la siguiente información sobre cada caso de prueba:  
  
-   Nombre: El nombre del caso de prueba.  
  
-   Creado: El caso de prueba fecha de creación.  
  
-   Modificado: El caso de prueba fecha de última modificación.  
  
-   Descripción: El caso de prueba descripciones.  
  
Los siguientes botones están disponibles en la página de casos de prueba:  
  
-   Haga clic en el **agregar** botón para ejecutar el Asistente de caso de prueba y crear una nueva prueba.  
  
-   Haga clic en el **quitar** botón para eliminar la prueba seleccionada en el repositorio. Cuando se elimina un caso de prueba, también se eliminan todos los resultados de pruebas relacionadas.  
  
-   Haga clic en el **editar** botón para ejecutar el Asistente de caso de prueba y cambiar la prueba seleccionada.  
  
-   Haga clic en el **ejecutar** para abrir el [ejecutar casos de prueba (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) cuadro de diálogo y ejecutar la prueba seleccionada.  
  
## <a name="test-results-repository"></a>Repositorio de resultados de pruebas  
También puede ver el repositorio de resultados de pruebas en el **los resultados de pruebas** página de la **repositorio de casos de prueba** ventana. Haga clic en **los resultados de pruebas...** desde el **Tester** menú.  
  
Puede utilizar dos filtros en **los resultados de pruebas** página:  
  
-   El filtro de nombre de caso de prueba: permite elegir los resultados de pruebas por el nombre del caso de prueba. Este filtro **todos los casos de prueba** valor permite mostrar los resultados de pruebas para todos los casos de prueba.  
  
-   El filtro de fecha de ejecución de caso de prueba: filtros de resultados de pruebas en la fecha de verano. Este filtro **período todos los** valor permite mostrar los resultados de pruebas para cualquier fecha de verano.  
  
La siguiente información sobre los resultados de pruebas se muestra en la cuadrícula.  
  
-   Nombre: nombre del caso de prueba.  
  
-   Guardar: Fecha de la prueba caso de verano.  
  
-   Resultados: Un breve resumen de la ejecución de pruebas (información sobre herramientas de la celda muestra un resumen completo de la ejecución de pruebas).  
  
Los siguientes botones están disponibles en la página de resultados de pruebas:  
  
-   Haga clic en el **vista** para abrir [ver informes de casos de prueba &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) de resultado de caso de prueba actual.  
  
-   Haga clic en el **eliminar** botón para eliminar el resultado de la prueba seleccionada  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Pruebas migran objetos de base de datos &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
