---
title: Ejecutar casos de prueba (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 80c335253aef5dd676ece990cb34feb5d67da829
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="running-test-cases-sybasetosql"></a>Ejecutar casos de prueba (SybaseToSQL)
Cuando el evaluador de SSMA se ejecuta un caso de prueba, ejecuta los objetos seleccionados para las pruebas y crea un informe sobre los resultados de la comprobación. Si los resultados son idénticos en ambas plataformas, la prueba fue correcta. La correspondencia de objetos entre Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se determina según la configuración de la asignación de esquema para el proyecto SSMA actual.  
  
Un requisito necesario para una prueba correcta es que todos los objetos de Sybase se convierten y se cargan en la base de datos de destino. También, se deben migrar los datos de tabla para que se sincroniza el contenido de las tablas en ambas plataformas.  
  
## <a name="run-test-case"></a>Ejecutar casos de prueba  
Para ejecutar el caso de prueba preparada:  
  
1.  Haga clic en el **ejecutar** botón.  
  
2.  En el **conectar para Sybase** cuadro de diálogo, escriba la información de conexión y, a continuación, haga clic en **conectar**.  
  
Una vez finalizada la prueba, se crea el informe de casos de prueba. Haga clic en el **informe** para ver el [ver informes de casos de prueba &#40; SybaseToSQL &#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). El resultado de la prueba (informe de casos de prueba) se almacena automáticamente en el [repositorios de pruebas usando &#40; SybaseToSQL &#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) para su uso posterior.  
  
## <a name="test-case-execution-steps"></a>Pasos de ejecución de caso de prueba  
  
### <a name="prerequisites"></a>Requisitos previos  
Evaluador de SSMA comprueba si se cumplen todos los requisitos previos para la ejecución de pruebas antes del inicio de la prueba. Si no se cumplen determinadas condiciones, aparece un mensaje de error.  
  
### <a name="initialization"></a>Inicialización  
En este paso, el evaluador de SSMA crea auxiliares objetos (tablas, desencadenadores y vistas) tanto en el Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Permiten que los cambios de seguimiento realizados en las tablas afectadas elegidas para comprobar si el modo de comparaciones de tabla es **cambia solo**.  
  
Se supone que la tabla comprobada se denomina USER_TABLE. Para este tipo de tabla, se crean los siguientes objetos auxiliares de Sybase.  
  
Los siguientes objetos se crean en Sybase en la base de datos SSMATESTER2005db o SSMATESTER2008db y en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en la base de datos de ssmatesterdb_syb.  
  
|Nombre|Tipo|Description|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
|USER_TABLE$ Aud|Table|Tabla donde se guardan las filas se eliminan y se sobrescriben.|  
|USER_TABLE$ AudID|Table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|Ver|Representación simplificada de las modificaciones de tablas.|  
|USER_TABLE$ nueva|Ver|Representación simplificada de filas insertadas y sobrescribir.|  
|USER_TABLE$ new_id|Ver|Identificación de filas insertadas y los cambios.|  
|USER_TABLE$ anterior|Ver|Representación simplificada de las filas se eliminan y se sobrescriben.|  
  
El siguiente objeto se crea en la base de datos de tabla comprobado en Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
|Nombre|Tipo|Description|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
  
### <a name="test-object-calls"></a>Llamadas de objeto de prueba  
En este paso, el evaluador de SSMA invoca cada objeto seleccionado para la prueba, compara los resultados y se muestra el informe.  
  
### <a name="finalization"></a>Finalización  
Durante la finalización de la herramienta de comprobación de SSMA limpia los objetos auxiliares creados en el **inicialización** paso.  
  
## <a name="next-step"></a>Paso siguiente  
[Ver informes de casos de prueba &#40; SybaseToSQL &#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Seleccionar y configurar los objetos a prueba &#40; SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Seleccionar y configurar los objetos afectados &#40; SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Pruebas migran objetos de base de datos &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

