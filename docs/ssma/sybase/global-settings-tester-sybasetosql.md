---
title: Configuración global (Tester) (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8091140978d417fa33beed187f055b26af2b9d31
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="global-settings-tester-sybasetosql"></a>Configuración global (Tester) (SybaseToSQL)
Use la página de herramienta de comprobación de la **configuración Global** cuadro de diálogo para especificar la configuración de pruebas de SSMA.  
  
Para acceder a la configuración de la herramienta de comprobación, en la **herramientas** menú, seleccione **configuración Global**y haga clic en **Tester** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Análisis de objeto pueden someterse a prueba**  
Esta configuración especifica si se debe realizar el análisis de los objetos pueden someterse a prueba. Seleccione **Sí** si desea que el evaluador de SSMA para analizar y buscar automáticamente los objetos dependientes. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  no  
  
**Tablas auxiliares de modo de ahorro**  
Esta configuración especifica cómo guardar las tablas auxiliares internas creadas durante la ejecución del caso de prueba. Siguientes opciones se pueden establecer para esta configuración concreta:  
  
1.  Eliminar siempre  
  
2.  Guarde siempre  
  
3.  Guardar si produce un error de comparación de la tabla  
  
4.  Pida el usuario si la comparación de la tabla no se pudo  
  
La opción establecida de forma predeterminada es: **siempre eliminar**.  
  
**Realizar la reversión de datos**  
Esta configuración especifica si se debe realizar una operación de reversión después de ejecutar cada caso de prueba. Conjunto de opciones de forma predeterminada es **No**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  no  
  
**Detener la ejecución de prueba tras el primer error**  
Esta configuración especifica si se debe detener la ejecución de caso de prueba actual, si se ha producido un error durante la ejecución. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  no  
  
## <a name="see-also"></a>Vea también  
[Finalizar la preparación del caso de prueba &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
