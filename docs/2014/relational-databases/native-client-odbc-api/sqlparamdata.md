---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 912d4b0a6f6a7565d62cb3f81f14ee4c99234974
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705934"
---
# <a name="sqlparamdata"></a>SQLParamData
  Cuando SQLParamData devuelve el *ValuePtrPtr* asociado a un parámetro con valores de tabla, la aplicación debe llamar a SQLPutData con *StrLen_Or_Ind*. Si *StrLen_Or_Ind* tiene un valor mayor que 0, significa que la aplicación está lista para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recopile los datos de parámetro para la siguiente fila de parámetro con valores de tabla. Si *StrLen_Or_Ind* tiene un valor de 0, significa que no hay más filas de datos para el parámetro con valores de tabla. Para obtener más información, vea [enlazar y transferencia de datos de parámetros con valores de tabla y valores de columna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
