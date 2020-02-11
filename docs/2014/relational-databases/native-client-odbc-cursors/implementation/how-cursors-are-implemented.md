---
title: Cómo se implementan los cursores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c92391b1d8874da3a8901ccc5c6245e48334241
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188519"
---
# <a name="how-cursors-are-implemented"></a>Cómo se implementan los cursores
  Las aplicaciones ODBC controlan el comportamiento de un cursor estableciendo uno o más atributos de instrucción antes de ejecutar una instrucción SQL. ODBC tiene dos maneras diferentes de especificar las características de un cursor:  
  
-   Tipo de cursor  
  
     Los tipos de cursor se establecen mediante el atributo SQL_ATTR_CURSOR_TYPE de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Los tipos de cursor de ODBC son de solo avance, estático, controlado por conjunto de claves, mixto y dinámico. Establecer el tipo de cursor fue el método original para especificar los cursores en ODBC.  
  
-   Comportamiento de los cursores  
  
     El comportamiento de los cursores se establece mediante los atributos SQL_ATTR_CURSOR_SCROLLABLE y SQL_ATTR_CURSOR_SENSITIVITY de **SQLSetStmtAttr**. Estos atributos se modelan en las palabras clave SCROLL y SENSITIVE definidas para la instrucción DECLARE CURSOR en los estándares ISO. Estas dos opciones ISO se introdujeron en la versión 3.0 de ODBC.  
  
 Las características de un cursor ODBC se deberían especificar con cualquiera de estos dos métodos, siendo preferente el uso de los tipos de cursor de ODBC.  
  
 Además de establecer el tipo de un cursor, las aplicaciones ODBC también establecen otras opciones, como el número de filas devueltas en cada captura, opciones de simultaneidad y niveles de aislamiento de transacción. Estas opciones se pueden establecer tanto para cursores de estilo ODBC (de solo avance, estático, controlado por conjunto de claves, mixto y dinámico) como para cursores de estilo ISO (desplazamiento y sensibilidad).  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite varias maneras de implementar físicamente los distintos tipos de cursores. El controlador implementa algunos tipos de cursores mediante un conjunto de resultados predeterminado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; implementa otros como cursores de servidor o mediante la Biblioteca de cursores ODBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar conjuntos de resultados predeterminados de SQL Server](using-sql-server-default-result-sets.md)  
  
-   [Utilizar cursores de servidor](using-server-cursors.md)  
  
-   [Biblioteca de cursores ODBC](odbc-cursor-library.md)  
  
## <a name="see-also"></a>Consulte también  
 [Usar cursores &#40;&#41;ODBC](../using-cursors-odbc.md)  
  
  
