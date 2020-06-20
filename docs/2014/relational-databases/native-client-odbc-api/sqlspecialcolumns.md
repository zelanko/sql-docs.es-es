---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: rothja
ms.author: jroth
ms.openlocfilehash: c36ff73606e95ed7ee5e713b81acf7c177a42563
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021574"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  Cuando se solicitan identificadores de fila (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** devuelve un conjunto de resultados vacío (ninguna fila de datos) para cualquier ámbito solicitado distinto de SQL_SCOPE_CURROW. El conjunto de resultados generado indica que las columnas solamente son válidas dentro de este ámbito.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite pseudocolumnas para identificadores. El conjunto de resultados de **SQLSpecialColumns** identificará todas las columnas como SQL_PC_NOT_PSEUDO.  
  
 **SQLSpecialColumns** se puede ejecutar en un cursor estático. Si se intenta ejecutar **SQLSpecialColumns** en un cursor actualizable (dinámico o controlado por conjunto de claves), devuelve SQL_SUCCESS_WITH_INFO para indicar que el tipo de cursor ha cambiado.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns admite características mejoradas de fecha y hora  
 Para obtener información sobre los valores devueltos para las columnas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH y DECIMAL_DIGTS para tipos de fecha y hora, vea [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información general, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>Compatibilidad con SQLSpecialColumns para el UDT CLR grandes  
 **SQLSpecialColumns** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLSpecialColumns función)](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
