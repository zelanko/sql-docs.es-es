---
title: SQLPrimaryKeys (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e026ae53e7b69e3a060d8fe42c8be70f5d4f43
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: 2 de nivel  
  
 Devuelve los nombres de columna que componen la clave principal de una tabla. La implementación del controlador ODBC de Visual FoxPro de **SQLPrimaryKeys** se comporta como sigue:  
  
-   Omite la *szTableOwner* y *cbTableOwner* argumentos.  
  
-   Sólo funciona en los orígenes de datos que son [bases de datos](../../odbc/microsoft/visual-foxpro-terminology.md). El controlador devuelve el error "El controlador no admite esta función" si el origen de datos es un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obtener más información, consulte [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) en el *referencia del programador de ODBC*.
