---
title: Ejecutar casos de prueba (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 664c2d3d4e1a1cea78bd93c748d9c17d2f1fe670
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833243"
---
# <a name="running-test-cases-sybasetosql"></a>Ejecución de casos de prueba (SybaseToSQL)
Cuando el evaluador de SSMA se ejecuta un caso de prueba, los objetos seleccionados para las pruebas se ejecuta y crea un informe sobre los resultados de la comprobación. Si los resultados son idénticos en ambas plataformas, la prueba fue correcta. La correspondencia de objetos entre Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se determina según la configuración de asignación de esquema para el proyecto SSMA actual.  
  
Un requisito necesario para una prueba correcta es que todos los objetos de Sybase se convierten y se cargan en la base de datos de destino. También, se deben migrar los datos de tabla para que se sincroniza el contenido de las tablas en ambas plataformas.  
  
## <a name="run-test-case"></a>Ejecutar casos de prueba  
Para ejecutar el caso de prueba preparada:  
  
1.  Haga clic en el **ejecutar** botón.  
  
2.  En el **conectarse a Sybase** cuadro de diálogo, escriba la información de conexión y, a continuación, haga clic en **Connect**.  
  
Una vez completada la prueba, se crea el informe de casos de prueba. Haga clic en el **informe** para ver el [ver informes de casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). El resultado de la prueba (informe de casos de prueba) se almacena automáticamente en el [utilizando repositorios de prueba &#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) para su uso posterior.  
  
## <a name="test-case-execution-steps"></a>Pasos de ejecución de casos de prueba  
  
### <a name="prerequisites"></a>Requisitos previos  
Evaluador de SSMA comprueba si se cumplen todos los requisitos previos para la ejecución de pruebas antes del inicio de la prueba. Si no se cumplen determinadas condiciones, aparecerá un mensaje de error.  
  
### <a name="initialization"></a>Inicialización  
En este paso, el evaluador de SSMA crea auxiliares objetos (tablas, desencadenadores y vistas) tanto en el Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Permiten que el seguimiento de los cambios realizado en las tablas afectadas elegidas para la comprobación de si es el modo de tabla comparaciones **cambia solo**.  
  
Suponga que la tabla comprobada se denomina USER_TABLE. Para este tipo de tabla, se crean los siguientes objetos auxiliares de Sybase.  
  
Los siguientes objetos se crean en Sybase en la base de datos SSMATESTER2005db o SSMATESTER2008db y a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos ssmatesterdb_syb.  
  
|Nombre|Tipo|Descripción|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
|USER_TABLE$ Aud|Table|Tabla donde se guardan las filas eliminadas y sobrescribir.|  
|USER_TABLE$ AudID|Table|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|Ver|Representación simplificada de las modificaciones de tabla.|  
|USER_TABLE$ nuevo|Ver|Representación simplificada de las filas insertadas y sobrescribir.|  
|USER_TABLE$ new_id|Ver|Identificación de las filas insertadas y modificadas.|  
|USER_TABLE$ antiguo|Ver|Representación simplificada de las filas eliminadas y sobrescribir.|  
  
El siguiente objeto se crea en la base de datos de tabla comprobado en Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre|Tipo|Descripción|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Desencadenador|Auditoría de los cambios en la tabla comprobado el desencadenador.|  
  
### <a name="test-object-calls"></a>Llamadas de objeto de prueba  
En este paso, el evaluador de SSMA invoca cada objeto seleccionado para la prueba, compara los resultados y muestra el informe.  
  
### <a name="finalization"></a>Finalización  
Durante la finalización de la herramienta de comprobación de SSMA limpia los objetos auxiliares creados en el **inicialización** paso.  
  
## <a name="next-step"></a>Paso siguiente  
[Visualización de informes de casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Selección y configuración de objetos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Selección y configuración de los objetos afectados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Pruebas con objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
