---
title: SQLSpecialColumns (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3128dca9f473008b5e5fcae234fd9ba119911e81
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Recupera el conjunto óptimo de columnas que identifica de forma única una fila de la tabla.  
  
 El controlador ODBC de Visual FoxPro devuelve las columnas que componen la clave principal en la tabla de FoxPro. (Consulte [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) Si se llama con *fColType* establecido en SQL_ROWVER, no hay columnas se devuelven. **SQLSpecialColumns** solo funciona para los orígenes de datos que son [bases de datos](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obtener más información, consulte [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) en el *referencia del programador de ODBC*.

