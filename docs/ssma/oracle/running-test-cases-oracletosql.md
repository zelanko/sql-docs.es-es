---
title: Ejecutar casos de prueba (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 537865967d0e43b7dd9501f9fbb7b9605f5b9367
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696754"
---
# <a name="running-test-cases-oracletosql"></a>Ejecución de casos de prueba (OracleToSQL)
Cuando el evaluador de SSMA se ejecuta un caso de prueba, los objetos seleccionados para las pruebas se ejecuta y crea un informe sobre los resultados de la comprobación. Si los resultados son idénticos en ambas plataformas, la prueba fue correcta. La correspondencia de objetos entre Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se determina según la configuración de asignación de esquema para el proyecto SSMA actual.  
  
Un requisito necesario para una prueba correcta es que todos los objetos de Oracle se convierten y se cargan en la base de datos de destino. También, se deben migrar los datos de tabla para que se sincroniza el contenido de las tablas en ambas plataformas.  
  
## <a name="run-test-case"></a>Ejecutar casos de prueba  
Para ejecutar el caso de prueba preparada:  
  
1.  Haga clic en el **ejecutar** botón.  
  
2.  En el **conectar con Oracle** cuadro de diálogo, escriba la información de conexión y, a continuación, haga clic en **Connect**.  
  
Una vez completada la prueba, se crea el informe de casos de prueba. Haga clic en el **informe** para ver el [informe casos de prueba](viewing-test-case-reports-oracletosql.md). El resultado de la prueba (informe de casos de prueba) se almacena automáticamente en el [repositorio de resultados de pruebas](using-test-repositories-oracletosql.md) para su uso posterior.  
  
## <a name="test-case-execution-steps"></a>Pasos de ejecución de casos de prueba  
  
### <a name="prerequisites"></a>Requisitos previos  
Evaluador de SSMA comprueba si se cumplen todos los requisitos previos para la ejecución de pruebas antes del inicio de la prueba. Si no se cumplen determinadas condiciones, aparecerá un mensaje de error.  
  
### <a name="initialization"></a>Inicialización  
En este paso, el evaluador de SSMA crea objetos auxiliares (tablas, desencadenadores y vistas) en el esquema SSMATESTER_ORACLE del servidor de Oracle. Le permiten el seguimiento de los cambios realizado en los objetos afectados elegidos para la comprobación.  
  
Suponga que la tabla comprobada se denomina USER_TABLE. Para este tipo de tabla, se crean los siguientes objetos auxiliares en Oracle.  
  
||||  
|-|-|-|  
|Nombre|Tipo|Descripción|  
|USER_TABLE$ Trg|desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
|USER_TABLE$ AUD|table|Tabla donde se guardan las filas eliminadas y sobrescribir.|  
|USER_TABLE$ AUDID|table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|ver|Representación simplificada de las modificaciones de tabla.|  
|USER_TABLE$ NUEVO|ver|Representación simplificada de las filas insertadas y sobrescribir.|  
|USER_TABLE$ NEW_ID|ver|Identificación de las filas insertadas y modificadas.|  
|USER_TABLE$ ANTIGUO|ver|Representación simplificada de las filas eliminadas y sobrescribir.|  
  
Se crea el siguiente objeto en el esquema de tabla comprobado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||||  
|-|-|-|  
|Nombre|Tipo|Descripción|  
|USER_TABLE$ Trg|desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
  
Y los siguientes objetos se crean en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en la base de datos ssmatesterdb.  
  
||||  
|-|-|-|  
|Nombre|Tipo|Descripción|  
|USER_TABLE$ Aud|table|Tabla donde se guardan las filas eliminadas y sobrescribir.|  
|USER_TABLE$ AudID|table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|ver|Representación simplificada de las modificaciones de tabla.|  
|USER_TABLE$ nuevo|ver|Representación simplificada de las filas insertadas y sobrescribir.|  
|USER_TABLE$ new_id|ver|Identificación de las filas insertadas y modificadas.|  
|USER_TABLE$ antiguo|ver|Representación simplificada de las filas eliminadas y sobrescribir.|  
  
### <a name="test-object-calls"></a>Llamadas de objeto de prueba  
En este paso, el evaluador de SSMA invoca cada objeto seleccionado para la prueba, compara los resultados y muestra el informe.  
  
### <a name="finalization"></a>Finalización  
Durante la finalización de la herramienta de comprobación de SSMA limpia los objetos auxiliares creados en el **inicialización** paso.  
  
## <a name="next-step"></a>Paso siguiente  
[Visualización de informes de casos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Vea también  
[Selección y configuración de objetos de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Selección y configuración de los objetos afectados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Pruebas con objetos de base de datos migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
