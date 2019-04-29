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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da50163b90d4a871c2524e1723797474386be8f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046679"
---
# <a name="sqlparamdata"></a>SQLParamData
  Cuando se devuelve SQLParamData el *ValuePtrPtr* asociado con un parámetro con valores de tabla, la aplicación debe llamar a SQLPutData con *StrLen_Or_Ind*. Si *StrLen_Or_Ind* tiene un valor mayor que 0, significa que la aplicación está lista para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client recopile los datos de parámetro para la siguiente fila de parámetro con valores de tabla. Si *StrLen_Or_Ind* tiene un valor de 0, significa que no hay más filas de datos para el parámetro con valores de tabla. Para obtener más información, consulte [enlace y Data Transfer of Table-Valued parámetros y valores de columna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
