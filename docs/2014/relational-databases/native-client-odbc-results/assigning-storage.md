---
title: Asignación de almacenamiento | Documentos de Microsoft
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
- column-wise binding [ODBC]
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLBindCol function
- storing data [ODBC]
- result sets [ODBC], storage
- SQL Server Native Client ODBC driver, data storage
- row-wise binding
- binding result sets [SQL Server Native Client]
- array binding
ms.assetid: 11c81955-5300-495f-925f-9256f2587b58
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eb77a63cb3522d86b40742780e44a141dc0a6c15
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196678"
---
# <a name="assigning-storage"></a>Asignar almacenamiento
  Una aplicación puede asignar almacenamiento para los resultados antes o después de ejecutar una instrucción SQL. Si una aplicación prepara o ejecuta primero la instrucción SQL, puede realizar consultas sobre el conjunto de resultados antes de asignar almacenamiento para los resultados. Por ejemplo, si no se conoce el conjunto de resultados, la aplicación debe recuperar el número de columnas para poder asignar almacenamiento al mismo.  
  
 Para asociar almacenamiento para una columna de datos, una aplicación llama [SQLBindCol](../native-client-odbc-api/sqlbindcol.md)y le pasa:  
  
-   El tipo al que deben convertirse los datos.  
  
-   La dirección de un búfer de salida para los datos.  
  
     La aplicación debe asignar este búfer, que debe ser lo suficientemente grande como para albergar los datos en el formato al que se conviertan.  
  
-   La longitud del búfer de salida.  
  
     Este valor se omite si los datos devueltos tienen un ancho fijo en C, como un entero, un número real o una estructura de fecha.  
  
-   La dirección de un búfer de almacenamiento donde devolver el número de bytes de los datos disponibles.  
  
 Una aplicación también puede enlazar las columnas del conjunto de resultados a matrices de variables de programa para que las filas del conjunto de resultados puedan capturarse en bloques. Existen dos tipos distintos de enlaces de matriz:  
  
-   El enlace de modo de columna finaliza cuando cada columna se enlaza a su propia matriz de variables.  
  
     El enlace se especifica mediante una llamada a [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con *atributo* establecido en SQL_ATTR_ROW_BIND_TYPE y *ValuePtr* establecido en SQL_BIND_BY_COLUMN. Todas las matrices deben tener el mismo número de elementos.  
  
-   El enlace de modo de fila finaliza cuando todos los parámetros de la instrucción SQL se enlazan como una unidad a una matriz de estructuras que contienen variables individuales para los parámetros.  
  
     El enlace se especifica mediante una llamada a **SQLSetStmtAttr** con *atributo* establecido en SQL_ATTR_ROW_BIND_TYPE y *ValuePtr* establecido en el tamaño de la explotación de estructura el columnas del conjunto de variables que va a recibir el resultado.  
  
 La aplicación también establece SQL_ATTR_ROW_ARRAY_SIZE en el número de elementos de las matrices de columnas o filas y establece SQL_ATTR_ROW_STATUS_PTR y SQL_ATTR_ROWS_FETCHED_PTR.  
  
## <a name="see-also"></a>Vea también  
 [Procesar resultados &#40;ODBC&#41;](processing-results-odbc.md)  
  
  