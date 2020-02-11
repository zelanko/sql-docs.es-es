---
title: Comprobación de coherencia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125539"
---
# <a name="consistency-check"></a>Comprobación de coherencia
El controlador realiza automáticamente una comprobación de coherencia cada vez que una aplicación establece el campo de SQL_DESC_DATA_PTR de APD, ARD o IPD. Cada vez que se establece este campo, el controlador comprueba que el valor del campo de SQL_DESC_TYPE y los valores aplicables al campo de SQL_DESC_TYPE en el mismo registro son válidos y coherentes.  
  
 Normalmente no se establece el campo de SQL_DESC_DATA_PTR de un IPD; sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. El valor en el que se establece el campo de SQL_DESC_DATA_PTR de IPD no se almacena realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**. la configuración solo se realiza para forzar la comprobación de coherencia. No se puede realizar una comprobación de coherencia en un IRD.  
  
 Para obtener más información sobre la comprobación de coherencia, vea [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
