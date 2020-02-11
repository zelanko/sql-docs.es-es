---
title: SQLSpecialColumns (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b690cceecb6c9980f5d84e96bccb1b02f014c026
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093095"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Recupera el conjunto óptimo de columnas que identifica de forma única una fila de la tabla.  
  
 El controlador ODBC de Visual FoxPro devuelve las columnas que componen la clave principal en la tabla de FoxPro. (Consulte [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)). Si se llama con *fColType* establecido en SQL_ROWVER, no se devuelve ninguna columna. **SQLSpecialColumns** solo funciona con orígenes de datos que son [bases](../../odbc/microsoft/visual-foxpro-terminology.md)de datos de.  
  
 Para obtener más información, vea [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) en la *Referencia del programador de ODBC*.
