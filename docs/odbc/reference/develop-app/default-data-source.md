---
title: Fuente de datos predeterminada ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305996"
---
# <a name="default-data-source"></a>Origen de datos predeterminado
El controlador puede seleccionar un origen de datos, denominado origen de datos predeterminado, en determinados casos en los que la aplicación no especifica explícitamente uno:  
  
-   En una llamada a **SQLConnect** donde el *ServerName* argumento es una cadena de longitud cero, un puntero nulo o DEFAULT.  
  
-   En una llamada a **SQLDriverConnect** donde *InConnectionString* especifica **DSN**.DEFAULT o especifica con la palabra clave **DSN** un origen de datos que no está contenido en la información del sistema.  
  
 Se define por el controlador cómo se especifica el origen de datos predeterminado. Esto puede implicar una acción administrativa y puede depender del usuario.
