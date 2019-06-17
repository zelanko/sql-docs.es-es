---
title: Configuración global (evaluador) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 0cbe66e8298053ef1682e25e97024fa0a96e9abb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62864906"
---
# <a name="global-settings-tester-oracletosql"></a>Configuración global (evaluador) (OracleToSQL)
Use la página de la herramienta de comprobación de la **configuración Global** cuadro de diálogo para especificar la configuración de pruebas de SSMA.  
  
Para obtener acceso a la configuración de la herramienta de comprobación, en el **herramientas** menú, seleccione **configuración Global**y haga clic en **evaluador** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Análisis de objeto comprobables**  
Esta configuración especifica si se debe realizar el análisis de los objetos que puede probar. Seleccione **Sí** si desea que el evaluador de SSMA para analizar y buscar automáticamente los objetos dependientes. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  No  
  
**Modo de ahorro de tablas auxiliares**  
Esta configuración especifica cómo se guardan las tablas auxiliares internas creadas durante la ejecución del caso de prueba. Siguientes opciones se pueden establecer para esta configuración concreta:  
  
1.  Eliminar siempre  
  
2.  Guarde siempre  
  
3.  Guardar el caso de error de comparación de la tabla  
  
4.  Pedir el usuario si la comparación de la tabla no se pudo  
  
La opción establecida de forma predeterminada es: **Eliminar siempre**.  
  
**Realizar reversión de datos**  
Esta configuración especifica si se debe realizar una operación de reversión después de ejecutar cada caso de prueba. Conjunto de opciones de forma predeterminada es **No**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  Sin  
  
**Detener la ejecución de pruebas tras el primer error**  
Esta configuración especifica si se debe detener la ejecución de caso de prueba actual, si se ha producido un error durante la ejecución. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  No  
  
## <a name="see-also"></a>Vea también  
[Finalización de la preparación del caso de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
