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
manager: shamikg
ms.openlocfilehash: f7e421774d3a09622835b181d5c053c994e905ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264414"
---
# <a name="global-settings-tester-oracletosql"></a>Configuración global (evaluador) (OracleToSQL)
Use la página de la herramienta de comprobación de la **configuración Global** cuadro de diálogo para especificar la configuración de pruebas de SSMA.  
  
Para obtener acceso a la configuración de la herramienta de comprobación, en el **herramientas** menú, seleccione **configuración Global**y haga clic en **evaluador** en la parte inferior del panel izquierdo.  
  
## <a name="options"></a>Opciones  
**Análisis de objeto comprobables**  
Esta configuración especifica si se debe realizar el análisis de los objetos que puede probar. Seleccione **Sí** si desea que el evaluador de SSMA para analizar y buscar automáticamente los objetos dependientes. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  Sin  
  
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
  
2.  No  
  
**Detener la ejecución de pruebas tras el primer error**  
Esta configuración especifica si se debe detener la ejecución de caso de prueba actual, si se ha producido un error durante la ejecución. Conjunto de opciones de forma predeterminada es **Sí**.  
  
Las siguientes opciones están disponibles para esta configuración:  
  
1.  Sí  
  
2.  Sin  
  
## <a name="see-also"></a>Vea también  
[Finalización de la preparación del caso de prueba &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
