---
title: Conversión de datos de parámetros con valores de tabla
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5e130fcc4a1ccc3303117ca34abdc6510e815e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297821"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversión de datos de parámetros con valores de tabla y otros errores y advertencias
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los valores de columna de parámetro con valores de tabla se pueden convertir entre tipos de cliente y de servidor de la misma manera que otros valores de parámetro y columna. Sin embargo, dado que un parámetro con valores de tabla puede contener varias columnas y filas, es importante poder identificar el valor real donde se produjo el error.  
  
 Cuando se detecta un error o una advertencia en una columna de parámetro con valores de tabla, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera un registro de diagnóstico. El mensaje de error contendrá el número de parámetro del parámetro con valores de tabla, más el ordinal de la columna y el número de fila. Una aplicación también puede utilizar los campos de diagnóstico SQL_DIAG_SS_TABLE_COLUMN_NUMBER y SQL_DIAG_SS_TABLE_ROW_NUMBER dentro de registros de diagnóstico para determinar qué valores están asociados a errores y advertencias. Estos campos de diagnóstico están disponibles en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.  
  
 Los componentes de mensaje y SQLSTATE de registros de diagnóstico cumplen los comportamientos de ODBC existentes en todos los demás aspectos. Es decir, a excepción de la información de identificación de parámetros, filas y columnas, los mensajes de error tienen los mismos valores para los parámetros con valores de tabla que para los parámetros que no tienen valores de tabla.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
