---
title: Uso de repositorios de prueba (SybaseToSQL) | Documentos de Microsoft
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
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c1278cdd2bbccc459bd93e16bfa1556ad95450ed
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-test-repositories-sybasetosql"></a>Uso de repositorios de prueba (SybaseToSQL)
Los almacenes de repositorio de pruebas de SSMA SSMA evaluador casos de prueba y los resultados de pruebas para su uso posterior. Los datos del repositorio se guardan en las tablas de SQL Server **TestCaseRepository** y **RunTestCaseResultRepository** en el esquema **ssma_sybase_utilities** de **ssmatesterdb_syb** base de datos.  
  
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
  
-   Haga clic en el **ejecutar** para abrir el [ejecutar casos de prueba &#40;SybaseToSQL&#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) cuadro de diálogo y ejecutar la prueba seleccionada.  
  
## <a name="test-results-repository"></a>Repositorio de resultados de pruebas  
También puede ver el repositorio de resultados de pruebas en el **los resultados de pruebas** página de la **repositorio de casos de prueba** ventana. Haga clic en **los resultados de pruebas...** desde el **Tester** menú.  
  
Puede utilizar dos filtros en **los resultados de pruebas** página:  
  
-   El filtro de nombre de caso de prueba: permite elegir los resultados de pruebas por el nombre del caso de prueba. Este filtro **todos los casos de prueba** valor permite mostrar los resultados de pruebas para todos los casos de prueba.  
  
-   El filtro de fecha de ejecución de caso de prueba: filtros de resultados de pruebas en la fecha de verano. Este filtro **período todos los** valor permite mostrar los resultados de pruebas para cualquier fecha de verano.  
  
La siguiente información sobre los resultados de pruebas se muestra en la cuadrícula.  
  
-   Nombre: nombre del caso de prueba.  
  
-   Iniciado: Fecha mayúscula de la ejecución de prueba.  
  
-   Resultado: Un breve resumen de la ejecución de pruebas (información sobre herramientas de la celda muestra un resumen completo de la ejecución de pruebas).  
  
Los siguientes botones están disponibles en la página de resultados de pruebas:  
  
-   Haga clic en el **vista** para abrir [ver informes de casos de prueba &#40;SybaseToSQL&#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) de resultado de caso de prueba actual.  
  
-   Haga clic en el **eliminar** botón para eliminar el resultado de la prueba seleccionada  
  
## <a name="see-also"></a>Vea también  
[Ejecutar casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Pruebas de objetos de base de datos migran &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
