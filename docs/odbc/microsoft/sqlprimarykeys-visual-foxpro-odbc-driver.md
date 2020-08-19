---
description: SQLPrimaryKeys (controlador ODBC de Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b333e10c7000a8a44e957e33d0c84a3b004f43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483348"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 2  
  
 Devuelve los nombres de columna que componen la clave principal de una tabla. La implementación del controlador ODBC de Visual FoxPro de **SQLPrimaryKeys** se comporta de la siguiente manera:  
  
-   Omite los argumentos *szTableOwner* y *cbTableOwner* .  
  
-   Solo funciona con orígenes de datos que son [bases](../../odbc/microsoft/visual-foxpro-terminology.md)de datos de. El controlador devuelve el error "el controlador no admite esta función" si el origen de datos es un directorio de [tablas libres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obtener más información, vea [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) en la *Referencia del programador de ODBC*.
