---
title: Usar parámetros de instrucciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8c359db9f39f659ac497adcf3bc6e343e1dd6796
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204597"
---
# <a name="using-statement-parameters"></a>Usar parámetros de instrucciones
  Un parámetro es una variable en una instrucción SQL que puede habilitar una aplicación ODBC:  
  
-   Proporcionando de forma eficaz valores para las columnas de una tabla.  
  
-   Mejorando la interacción del usuario para construir criterios de consulta.  
  
-   Administrar **texto**, **ntext**, y **imagen** datos y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-tipos de datos C específicos.  
  
 Por ejemplo, un **elementos** tabla tiene columnas denominadas **PartID**, **descripción**, y **precio**. Para agregar una parte sin parámetros se requiere la construcción de una instrucción SQL como:  
  
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
  
-   [Parámetros de enlace](using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  