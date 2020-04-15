---
title: Desplazamiento relativo y absoluto ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300105"
---
# <a name="relative-and-absolute-scrolling"></a>Desplazamiento relativas y absolutas
La mayoría de las opciones de desplazamiento en **SQLFetchScroll** colocan el cursor en relación con la posición actual o en una posición absoluta. **SQLFetchScroll** admite la obtención de los conjuntos de filas siguiente, anterior, primero y último, así como la obtención relativa (capturar el conjunto de filas *n* filas desde el inicio del conjunto de filas actual) y la obtención absoluta (capturar el conjunto de filas a partir de la fila *n*). Si *n* es negativo en una captura absoluta, las filas se cuentan desde el final del conjunto de resultados. Por lo tanto, una captura absoluta de la fila -1 significa capturar el conjunto de filas que comienza con la última fila del conjunto de resultados.  
  
 Los cursores dinámicos detectan filas insertadas y eliminadas del conjunto de resultados, por lo que no hay una manera fácil para que los cursores dinámicos recuperen la fila en un número determinado que no sea la lectura desde el principio del conjunto de resultados, lo que es probable que sea lento. Además, la obtención absoluta no es muy útil en los cursores dinámicos porque los números de fila cambian a medida que se insertan y eliminan filas; por lo tanto, capturar sucesivamente el mismo número de fila puede producir filas diferentes.  
  
 Las aplicaciones que usan **SQLFetchScroll** solo para sus capacidades de cursor de bloque, como informes, es probable que pasen a través del conjunto de resultados una sola vez, utilizando solo la opción para capturar el siguiente conjunto de filas. Las aplicaciones basadas en pantalla, por otro lado, pueden aprovechar todas las capacidades de **SQLFetchScroll**. Si la aplicación establece el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla y enlaza los búferes de pantalla al conjunto de resultados, puede traducir las operaciones de la barra de desplazamiento directamente a las llamadas a **SQLFetchScroll**.  
  
|Funcionamiento de la barra de desplazamiento|Opción de desplazamiento de SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Re Pág|SQL_FETCH_PRIOR|  
|Página abajo|SQL_FETCH_NEXT|  
|Línea arriba|SQL_FETCH_RELATIVE con *FetchOffset* igual a -1|  
|Línea abajo|SQL_FETCH_RELATIVE con *FetchOffset* igual a 1|  
|Cuadro de desplazamiento en la parte superior|SQL_FETCH_FIRST|  
|Cuadro de desplazamiento en la parte inferior|SQL_FETCH_LAST|  
|Posición del cuadro de desplazamiento aleatoria|SQL_FETCH_ABSOLUTE|  
  
 Estas aplicaciones también necesitan colocar el cuadro de desplazamiento después de una operación de desplazamiento, que requiere el número de fila actual y el número de filas. Para el número de fila actual, las aplicaciones pueden realizar un seguimiento del número de fila actual o llamar a **SQLGetStmtAttr** con el atributo SQL_ATTR_ROW_NUMBER para recuperarlo.  
  
 El número de filas del cursor, que es el tamaño del conjunto de resultados, está disponible como el campo SQL_DIAG_CURSOR_ROW_COUNT del encabezado de diagnóstico. El valor de este campo se define solo después de llamar a **SQLExecute**, **SQLExecDirect**o **SQLMoreResult** . Este recuento puede ser un recuento aproximado o un recuento exacto, dependiendo de las capacidades del controlador. La compatibilidad del controlador se puede determinar llamando a **SQLGetInfo** con los tipos de información de atributos de cursor y comprobando si se devuelve el SQL_CA2_CRC_APPROXIMATE o SQL_CA2_CRC_EXACT bit para el tipo de cursor.  
  
 Nunca se admite un recuento de filas exacto para un cursor dinámico. Para otros tipos de cursores, el controlador puede admitir recuentos de filas exactos o aproximados, pero no ambos. Si el controlador no admite recuentos de filas exactos ni aproximados para un tipo de cursor específico, el campo SQL_DIAG_CURSOR_ROW_COUNT contiene el número de filas que se han capturado hasta ahora. Independientemente de lo que admita el controlador, **SQLFetchScroll** con una *operación* de SQL_FETCH_LAST hará que el campo de SQL_DIAG_CURSOR_ROW_COUNT contenga el recuento de filas exacto.
