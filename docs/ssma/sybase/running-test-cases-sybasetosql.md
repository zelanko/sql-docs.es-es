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
ms.openlocfilehash: 73047e0741d4dee12ecec3e83df308e3f7abd343
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68021020"
---
# <a name="running-test-cases-sybasetosql"></a>Ejecución de casos de prueba (SybaseToSQL)
Cuando SSMA Tester ejecuta un caso de prueba, ejecuta los objetos seleccionados para las pruebas y crea un informe sobre los resultados de la comprobación. Si los resultados son idénticos en ambas plataformas, la prueba se realizó correctamente. La correspondencia de objetos entre Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se determina según la configuración de asignación de esquemas del proyecto SSMA actual.  
  
Un requisito necesario para una prueba correcta es que todos los objetos de Sybase se convierten y se cargan en la base de datos de destino. Además, los datos de la tabla se deben migrar para que el contenido de las tablas en ambas plataformas esté sincronizado.  
  
## <a name="run-test-case"></a>Ejecutar caso de prueba  
Para ejecutar el caso de prueba preparado:  
  
1.  Haga clic en el botón **Ejecutar**.  
  
2.  En el cuadro de diálogo **conectar a Sybase** , escriba la información de conexión y, a continuación, haga clic en **conectar**.  
  
Una vez finalizada la prueba, se crea el informe de casos de prueba. Haga clic en el botón **Informe** para ver los [informes de casos de prueba de visualización &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). El resultado de la prueba (informe de casos de prueba) se almacena automáticamente en el [uso de repositorios de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md) para su uso posterior.  
  
## <a name="test-case-execution-steps"></a>Pasos de ejecución del caso de prueba  
  
### <a name="prerequisites"></a>Prerrequisitos  
SSMA Tester comprueba si se cumplen todos los requisitos previos para la ejecución de pruebas antes de iniciar la prueba. Si no se cumplen algunas condiciones, aparece un mensaje de error.  
  
### <a name="initialization"></a>Inicialización  
En este paso, SSMA tester crea objetos auxiliares (tablas, desencadenadores y vistas) tanto en Sybase como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en. Permiten realizar cambios en el seguimiento de las tablas afectadas seleccionadas para la comprobación si el modo de comparación de tablas **solo cambia**.  
  
Supongamos que la tabla comprobada se denomina USER_TABLE. Para este tipo de tabla, se crean los siguientes objetos auxiliares en Sybase.  
  
Los objetos siguientes se crean en Sybase en la base de datos SSMATESTER2005db o SSMATESTER2008db [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en la base de datos ssmatesterdb_syb.  
  
|Nombre|Tipo|Descripción|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|Desencadenador|Desencadenador de auditoría de los cambios en la tabla comprobada.|  
|USER_TABLE $ AUD|Tabla|Tabla donde se guardan las filas eliminadas y sobrescritas.|  
|USER_TABLE $ AudID|Tabla|Tabla donde se guardan las filas nuevas y modificadas.|  
|USER_TABLE|Ver|Representación simplificada de las modificaciones de la tabla.|  
|USER_TABLE $ New|Ver|Representación simplificada de filas insertadas y sobrescritas.|  
|USER_TABLE $ new_id|Ver|Identificación de las filas insertadas y modificadas.|  
|USER_TABLE $ Old|Ver|Representación simplificada de filas eliminadas y reemplazadas.|  
  
El siguiente objeto se crea en la base de datos de la tabla comprobado en Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre|Tipo|Descripción|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|Desencadenador|Desencadenador de auditoría de los cambios en la tabla comprobada.|  
  
### <a name="test-object-calls"></a>Llamadas a objetos de prueba  
En este paso, SSMA Tester invoca cada objeto seleccionado para las pruebas, compara los resultados y muestra el informe.  
  
### <a name="finalization"></a>Finalización  
Durante la finalización, el evaluador de SSMA limpia los objetos auxiliares creados en el paso de **inicialización** .  
  
## <a name="next-step"></a>siguiente paso  
[Ver informes de casos de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Seleccionar y configurar objetos para probar &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Seleccionar y configurar objetos afectados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Probar objetos de base de datos migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
