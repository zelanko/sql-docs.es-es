---
title: Ejecutar casos de prueba (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8fd2e06a9d9dcaa243876638f405bcc78c6a9d33
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="running-test-cases-oracletosql"></a>Ejecutar casos de prueba (OracleToSQL)
Cuando el evaluador de SSMA se ejecuta un caso de prueba, ejecuta los objetos seleccionados para las pruebas y crea un informe sobre los resultados de la comprobación. Si los resultados son idénticos en ambas plataformas, la prueba fue correcta. La correspondencia de objetos entre Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se determina según la configuración de la asignación de esquema para el proyecto SSMA actual.  
  
Un requisito necesario para una prueba correcta es que todos los objetos de Oracle se convierten y se cargan en la base de datos de destino. También, se deben migrar los datos de tabla para que se sincroniza el contenido de las tablas en ambas plataformas.  
  
## <a name="run-test-case"></a>Ejecutar casos de prueba  
Para ejecutar el caso de prueba preparada:  
  
1.  Haga clic en el **ejecutar** botón.  
  
2.  En el **conectar con Oracle** cuadro de diálogo, escriba la información de conexión y, a continuación, haga clic en **conectar**.  
  
Una vez finalizada la prueba, se crea el informe de casos de prueba. Haga clic en el **informe** para ver el [informe casos de prueba](http://msdn.microsoft.com/en-us/8da14323-9dd6-4019-bf79-3e8b972a9bc0). El resultado de la prueba (informe de casos de prueba) se almacena automáticamente en el [repositorio de resultados de pruebas](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4) para su uso posterior.  
  
## <a name="test-case-execution-steps"></a>Pasos de ejecución de caso de prueba  
  
### <a name="prerequisites"></a>Requisitos previos  
Evaluador de SSMA comprueba si se cumplen todos los requisitos previos para la ejecución de pruebas antes del inicio de la prueba. Si no se cumplen determinadas condiciones, aparece un mensaje de error.  
  
### <a name="initialization"></a>Inicialización  
En este paso, SSMA evaluador crea objetos auxiliares (tablas, desencadenadores y vistas) en el esquema SSMATESTER_ORACLE del servidor de Oracle. Permiten que los cambios de seguimiento realizados en los objetos afectados elegidos para la comprobación.  
  
Se supone que la tabla comprobada se denomina USER_TABLE. Para este tipo de tabla, se crean los siguientes objetos auxiliares en Oracle.  
  
||||  
|-|-|-|  
|Nombre|Tipo|Description|  
|USER_TABLE$ Trg|desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
|USER_TABLE$ AUD|table|Tabla donde se guardan las filas se eliminan y se sobrescriben.|  
|USER_TABLE$ AUDID|table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|ver|Representación simplificada de las modificaciones de tablas.|  
|USER_TABLE$ NUEVOS|ver|Representación simplificada de filas insertadas y sobrescribir.|  
|USER_TABLE$ NEW_ID|ver|Identificación de filas insertadas y los cambios.|  
|USER_TABLE$ ANTERIOR|ver|Representación simplificada de las filas se eliminan y se sobrescriben.|  
  
Se crea el siguiente objeto en el esquema de tabla comprobado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
||||  
|-|-|-|  
|Nombre|Tipo|Description|  
|USER_TABLE$ Trg|desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
  
Y se crean los siguientes objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]en la base de datos de ssmatesterdb.  
  
||||  
|-|-|-|  
|Nombre|Tipo|Description|  
|USER_TABLE$ Aud|table|Tabla donde se guardan las filas se eliminan y se sobrescriben.|  
|USER_TABLE$ AudID|table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|ver|Representación simplificada de las modificaciones de tablas.|  
|USER_TABLE$ nueva|ver|Representación simplificada de filas insertadas y sobrescribir.|  
|USER_TABLE$ new_id|ver|Identificación de filas insertadas y los cambios.|  
|USER_TABLE$ anterior|ver|Representación simplificada de las filas se eliminan y se sobrescriben.|  
  
### <a name="test-object-calls"></a>Llamadas de objeto de prueba  
En este paso, el evaluador de SSMA invoca cada objeto seleccionado para la prueba, compara los resultados y se muestra el informe.  
  
### <a name="finalization"></a>Finalización  
Durante la finalización de la herramienta de comprobación de SSMA limpia los objetos auxiliares creados en el **inicialización** paso.  
  
## <a name="next-step"></a>Paso siguiente  
[Ver informes de casos de prueba &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Seleccionar y configurar los objetos para pruebas &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Seleccionar y configurar afectados objetos &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Pruebas migran objetos de base de datos &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
