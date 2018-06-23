---
title: SQLNumResultCols | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 73ac3425eab1a4c19130352ef566153eb6c34e53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105362"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Las instrucciones ejecutadas, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client no tiene acceso al servidor para notificar el número de columnas en un conjunto de resultados. En este caso, `SQLNumResultCols` no provoca un ida y vuelta del servidor. Al igual que [SQLDescribeCol](sqldescribecol.md) y [SQLColAttribute](sqlcolattribute.md), al llamar a `SQLNumResultCols` en preparado, pero las instrucciones ejecutadas no genera un ida y vuelta del servidor.  
  
 Cuando una instrucción o un lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que el número de columnas del conjunto de resultados cambie de un conjunto a otro. `SQLNumResultCols` se debe llamar para cada conjunto. Cuando el número de columnas cambia, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre el control de resultados múltiples conjuntos devuelve, vea [SQLMoreResults](sqlmoreresults.md).  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLNumResultCols obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLNumResultCols en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [de detección de metadatos](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLNumResultCols (función)](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  