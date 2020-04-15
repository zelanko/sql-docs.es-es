---
title: Uso de parámetros de instrucción ? Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74cd70bcd9107d68551dc3f82eb1e01f76a549b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297907"
---
# <a name="using-statement-parameters"></a>Usar parámetros de instrucciones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un parámetro es una variable en una instrucción SQL que puede habilitar una aplicación ODBC:  
  
-   Proporcionando de forma eficaz valores para las columnas de una tabla.  
  
-   Mejorando la interacción del usuario para construir criterios de consulta.  
  
-   Gestione los datos de **texto,** **ntext**e **imagen** y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los tipos de datos C específicos.  
  
 Por ejemplo, una tabla **Parts** tiene columnas denominadas **PartID**, **Description**y **Price**. Para agregar una parte sin parámetros se requiere la construcción de una instrucción SQL como:  
  
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
  
-   [Enlazar parámetros](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de consultas &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
