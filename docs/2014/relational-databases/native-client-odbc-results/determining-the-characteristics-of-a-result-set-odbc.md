---
title: Determinar las características de un conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
author: rothja
ms.author: jroth
ms.openlocfilehash: 5957092cdddfbcbce904d9a6483914672565d337
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999109"
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>Determinar las características de un conjunto de resultados (ODBC)
  Los metadatos son datos que describen otros datos. Por ejemplo, los metadatos de conjunto de resultados describen las características de un conjunto de resultados, como el número de columnas del conjunto de resultados, los tipos de datos de esas columnas, sus nombres, la precisión y la nulabilidad.  
  
 ODBC proporciona metadatos a las aplicaciones mediante las funciones de API de catálogo. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client implementa muchas de las funciones de catálogo de la API de ODBC como llamadas a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimiento de catálogo correspondiente.  
  
 Las aplicaciones requieren metadatos para la mayoría de las operaciones de conjunto de resultados. Por ejemplo, la aplicación utiliza el tipo de datos de una columna para determinar qué tipo de variable se ha de enlazar a esa columna. Utiliza la longitud de bytes de una columna de caracteres para determinar cuánto espacio debe tener para mostrar datos de esa columna. El modo en que una aplicación determina los metadatos de una columna depende del tipo de la aplicación.  
  
 Las aplicaciones verticales suelen funcionar con tablas predefinidas y realizan operaciones predefinidas en esas tablas. Dado que los metadatos de conjunto de resultados para dichas aplicaciones se definen antes incluso de que el programador escriba y controle la aplicación, pueden estar codificados de forma rígida en la aplicación. Por ejemplo, si una columna Id. de pedido se define como un entero de 4 bytes en el origen de datos, la aplicación siempre puede enlazar un entero de 4 bytes a esa columna. Cuando los metadatos están codificados de forma rígida en la aplicación, un cambio en las tablas utilizadas por la aplicación suele implicar un cambio en el código de la aplicación.  
  
 En aplicaciones genéricas, especialmente en aplicaciones que admiten consultas ad hoc, los metadatos de los conjuntos de resultados que crean suelen desconocerse hasta la ejecución.  
  
 Para determinar las características de un conjunto de resultados, una aplicación puede llamar a los siguientes elementos:  
  
-   [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) para determinar el número de columnas que ha devuelto una solicitud.  
  
-   [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) o [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) para describir una columna en el conjunto de resultados.  
  
 Una aplicación bien diseñada se escribe con la suposición de que el conjunto de resultados es desconocido y utiliza la información devuelta por estas funciones para enlazar las columnas del conjunto de resultados. Una aplicación puede llamar a estas funciones en cualquier momento posterior a la preparación o ejecución de una instrucción. Sin embargo, para obtener un rendimiento óptimo, una aplicación debe llamar a **SQLColAttribute**, **SQLDescribeCol**y **SQLNumResultCols** después de ejecutar una instrucción.  
  
 Puede tener varias llamadas simultáneas a metadatos. El controlador ODBC puede llamar a los procedimientos de catálogo del sistema que subyacen en las implementaciones de API de catálogo de ODBC mientras está utilizando los cursores de servidor estáticos. Esto permite a las aplicaciones procesar simultáneamente varias llamadas a funciones de catálogo de ODBC.  
  
 Si una aplicación utiliza un conjunto de metadatos concreto más de una vez, probablemente resultará beneficioso almacenar en memoria caché la información en variables privadas la primera vez que se obtenga. Esto evita la realización de llamadas posteriores a las funciones de catálogo de ODBC para obtener la misma información, lo que obliga al controlador a realizar viajes de ida y vuelta al servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Procesar los resultados &#40;ODBC&#41;](processing-results-odbc.md)  
  
  
