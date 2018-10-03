---
title: Valor predeterminado el origen de datos | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619573"
---
# <a name="default-data-source"></a>Origen de datos predeterminado
El controlador puede seleccionar un origen de datos, denominado el origen de datos de forma predeterminada, en algunos casos donde la aplicación no especifica explícitamente uno:  
  
-   En una llamada a **SQLConnect** donde el *ServerName* argumento es una cadena de longitud cero, un puntero nulo o predeterminado.  
  
-   En una llamada a **SQLDriverConnect** donde *InConnectionString* cualquiera especifica **DSN**= DEFAULT o se especifica con el **DSN** palabra clave un origen de datos que no se encuentra en la información del sistema.  
  
 Es definido por el controlador de cómo se especifica el origen de datos de forma predeterminada. Esto puede implicar una acción administrativa y es posible que dependen del usuario.
