---
title: Los datos del parámetro con valores de tabla de conversión y otros errores y advertencias | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2fc0e9889c5872280ef4d5f0baf00f84b88ef99
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176275"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversión de datos de parámetros con valores de tabla y otros errores y advertencias
  Los valores de columna de parámetro con valores de tabla se pueden convertir entre tipos de cliente y de servidor de la misma manera que otros valores de parámetro y columna. Sin embargo, dado que un parámetro con valores de tabla puede contener varias columnas y filas, es importante poder identificar el valor real donde se produjo el error.  
  
 Cuando se detecta un error o una advertencia en una columna de parámetro con valores de tabla, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera un registro de diagnóstico. El mensaje de error contendrá el número de parámetro del parámetro con valores de tabla, más el ordinal de la columna y el número de fila. Una aplicación también puede utilizar los campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER y SQL_DIAG_SS_TABLE_ROW_NUMBER dentro de registros de diagnóstico para determinar qué valores están asociados a errores y advertencias. Estos campos de diagnóstico están disponibles en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.  
  
 Los componentes de mensaje y SQLSTATE de registros de diagnóstico cumplen los comportamientos de ODBC existentes en todos los demás aspectos. Es decir, salvo la información de identificación de parámetro, fila y columna, los mensajes de error tienen los mismos valores para parámetros con valores de tabla que tendrían para parámetros que no tengan valores de tabla.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
