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
manager: craigg
ms.openlocfilehash: cb73d8a4de482f24eae5794232019af9890e3624
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727793"
---
# <a name="consistency-check"></a>Comprobación de coherencia
Se realiza una comprobación de coherencia por el controlador automáticamente cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR del APD, descartar o IPD. Cada vez que este campo se establece, el controlador comprueba que el valor del campo SQL_DESC_TYPE y los valores aplicables para el campo SQL_DESC_TYPE en el mismo registro son válidos y coherentes.  
  
 El campo SQL_DESC_DATA_PTR de un IPD no se establece normalmente; Sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. El valor establecido en el campo SQL_DESC_DATA_PTR de la IPD no se almacena realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**; la configuración se realiza solo para forzar la comprobación de coherencia. No se puede realizar una comprobación de coherencia en un IRD.  
  
 Para obtener más información sobre la comprobación de coherencia, consulte [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
