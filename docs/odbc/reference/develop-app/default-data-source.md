---
title: Origen de datos predeterminado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fb016ac7597617b119834e20ffd9e12bd648dc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076851"
---
# <a name="default-data-source"></a>Origen de datos predeterminado
El controlador puede seleccionar un origen de datos, denominado origen de datos predeterminado, en ciertos casos en los que la aplicación no especifica explícitamente uno:  
  
-   En una llamada a **SQLConnect** donde el argumento *ServerName* es una cadena de longitud cero, un puntero NULL o default.  
  
-   En una llamada a **SQLDriverConnect** , donde *inconnectionstring* especifica **DSN**= default o especifica con la palabra clave **DSN** un origen de datos que no está incluido en la información del sistema.  
  
 Está definido por el controlador cómo se especifica el origen de datos predeterminado. Esto puede implicar una acción administrativa y puede depender del usuario.
