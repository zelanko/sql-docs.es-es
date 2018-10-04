---
title: SQLPrimaryKeys (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3eeafa338fea31741609e6f9a9b32a4128ebd87d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765613"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Devuelve los nombres de columna que componen la clave principal de una tabla. La implementación del controlador ODBC de Visual FoxPro de **SQLPrimaryKeys** se comporta como sigue:  
  
-   Omite la *szTableOwner* y *cbTableOwner* argumentos.  
  
-   Solo funciona para los orígenes de datos que son [bases de datos](../../odbc/microsoft/visual-foxpro-terminology.md). El controlador devuelve el error "El controlador no admite esta función" si el origen de datos es un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obtener más información, consulte [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) en el *referencia del programador de ODBC*.
