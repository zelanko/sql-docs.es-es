---
title: Comprobación de la consistencia ( Consistency Check) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299005"
---
# <a name="consistency-check"></a>Comprobación de coherencia
El controlador realiza automáticamente una comprobación de coherencia cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR del APD, ARD o IPD. Siempre que se establece este campo, el controlador comprueba que el valor del campo SQL_DESC_TYPE y los valores aplicables al campo SQL_DESC_TYPE del mismo registro son válidos y coherentes.  
  
 El campo SQL_DESC_DATA_PTR de una IPD no se establece normalmente; sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. El valor en el que se establece el campo SQL_DESC_DATA_PTR de la IPD no se almacena realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**; el ajuste se realiza únicamente para forzar la comprobación de coherencia. No se puede realizar una comprobación de coherencia en un IRD.  
  
 Para obtener más información sobre la comprobación de coherencia, vea [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
