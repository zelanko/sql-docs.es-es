---
title: SQLParamData | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 57b45032038f81fe6e2e15202db7b8c790ca4716
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856923"
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cuando se devuelve SQLParamData el *ValuePtrPtr* asociado con un parámetro con valores de tabla, la aplicación debe llamar a SQLPutData con *StrLen_Or_Ind*. Si *StrLen_Or_Ind* tiene un valor mayor que 0, significa que la aplicación está lista para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recopile datos de parámetro para la siguiente fila de parámetro con valores de tabla. Si *StrLen_Or_Ind* tiene un valor de 0, significa que no hay más filas de datos para el parámetro con valores de tabla. Para obtener más información, consulte [enlace y Data Transfer of Table-Valued parámetros y valores de columna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
