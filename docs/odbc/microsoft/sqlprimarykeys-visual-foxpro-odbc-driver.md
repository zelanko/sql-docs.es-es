---
title: SQLPrimaryKeys (Controlador ODBC de Visual FoxPro) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301550"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 2  
  
 Devuelve los nombres de columna que componen la clave principal de una tabla. La implementación del controlador ODBC de Visual FoxPro de **SQLPrimaryKeys** se comporta de la siguiente manera:  
  
-   Omite los argumentos *szTableOwner* y *cbTableOwner.*  
  
-   Solo funciona para orígenes de datos que son bases de [datos.](../../odbc/microsoft/visual-foxpro-terminology.md) El controlador devuelve el error "Driver does not support this function" si el origen de datos es un directorio de [tablas libres.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 Para obtener más información, vea [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) en la *referencia del programador ODBC*.
