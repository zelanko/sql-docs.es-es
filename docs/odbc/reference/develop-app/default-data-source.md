---
title: Valor predeterminado de origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 256d200ce0cb7b64fd011bdba343ca0aae292232
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="default-data-source"></a>Origen de datos predeterminado
El controlador puede seleccionar un origen de datos, denominado el origen de datos de forma predeterminada, en ciertos casos donde la aplicación no especifica explícitamente uno:  
  
-   En una llamada a **SQLConnect** donde el *ServerName* argumento es una cadena de longitud cero, un puntero null o DEFAULT.  
  
-   En una llamada a **SQLDriverConnect** donde *InConnectionString* cualquiera especifica **DSN**= valor predeterminado o se especifica con el **DSN** palabra clave un origen de datos que no se encuentra en la información del sistema.  
  
 Es definido por el controlador cómo se especifica el origen de datos predeterminado. Esto puede implicar una acción administrativa y puede depender del usuario.
