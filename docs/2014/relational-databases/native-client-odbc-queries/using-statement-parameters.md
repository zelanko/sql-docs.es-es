---
title: Usar parámetros de instrucciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a16f070623503dcb17788bc75bd5695bc1584d7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200247"
---
# <a name="using-statement-parameters"></a>Usar parámetros de instrucciones
  Un parámetro es una variable en una instrucción SQL que puede habilitar una aplicación ODBC:  
  
-   Proporcionando de forma eficaz valores para las columnas de una tabla.  
  
-   Mejorando la interacción del usuario para construir criterios de consulta.  
  
-   Administrar **texto**, **ntext**, y **imagen** datos y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-tipos de datos C específicos.  
  
 Por ejemplo, un **partes** tabla tiene columnas denominadas **PartID**, **descripción**, y **precio**. Para agregar una parte sin parámetros se requiere la construcción de una instrucción SQL como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Aunque esta instrucción es aceptable para insertar una fila con un conjunto conocido de valores, resulta complicado cuando se requiere que una aplicación inserte varias filas. ODBC soluciona esto permitiendo que una aplicación reemplace cualquier valor de datos en una instrucción SQL mediante un creador de parámetro. Esto se indica mediante un signo de interrogación (?). En el ejemplo siguiente, tres valores de datos se reemplazan con marcadores de parámetros:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Los marcadores de parámetros se enlazan a variables de aplicación. Para insertar una nueva fila, la aplicación únicamente tiene que establecer los valores de las variables y ejecutar la instrucción. Después, el controlador recupera los valores actuales de las variables y los envía al origen de datos. Si se ejecuta la instrucción varias veces, la aplicación puede hacer que el proceso mejore al preparar la instrucción.  
  
 Cada número ordinal asignado a los parámetros de izquierda a derecha hace referencia a su marcador de parámetro. El marcador de parámetros del extremo izquierdo de una instrucción SQL tiene un valor ordinal de 1; el siguiente es el ordinal 2, etc.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Enlazar parámetros](using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
