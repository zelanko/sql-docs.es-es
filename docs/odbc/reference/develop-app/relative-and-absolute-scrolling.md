---
title: Desplazamiento relativas y absolutas | Documentos de Microsoft
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
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41155a5536493ba77941855e0283011ccda7d1a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="relative-and-absolute-scrolling"></a>Desplazamiento relativas y absolutas
La mayoría de las opciones de desplazamiento en **SQLFetchScroll** coloque el cursor en relación con la posición actual o a una posición absoluta. **SQLFetchScroll** admite la captura de la siguiente, anterior, primero y último conjuntos de filas, como una captura relativa bien como (capturar el conjunto de filas *n* filas desde el principio del conjunto de filas actual) y una captura absoluta (el conjunto de filas a partir de fetch en la fila *n*). Si *n* es negativo en una captura absoluta, las filas se cuentan desde el final del conjunto de resultados. Por lo tanto, una captura absoluta de fila -1 significa que se capturará el conjunto de filas que comienza por la última fila del conjunto de resultados.  
  
 Los cursores dinámicos detectan filas insertadas en y eliminadas del conjunto de resultados, así que no hay ninguna manera fácil para los cursores dinámicos recuperar la fila en un número determinado que no sea de lectura desde el principio del conjunto de resultados, que es probable que sea lenta. Además, una captura absoluta no es muy útil en los cursores dinámicos porque los números de fila cambiarán como filas se insertan o eliminan; por lo tanto, consecutivamente obtener el mismo número de filas puede generar filas diferentes.  
  
 Las aplicaciones que utilizan **SQLFetchScroll** únicamente para su bloque de capacidades de cursor, como informes, están probable que atraviesen el conjunto de resultados de una sola vez, utilizando solo la opción para capturar el siguiente conjunto de filas. Las aplicaciones basadas en la pantalla, por otro lado, pueden aprovechar todas las capacidades de **SQLFetchScroll**. Si la aplicación establece el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla y enlaza los búferes de pantalla al conjunto de resultados, pueden traducir las operaciones de la barra de desplazamiento directamente en llamadas a **SQLFetchScroll**.  
  
|Funcionamiento de la barra de desplazamiento|Opción de desplazamiento de SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Re Pág|SQL_FETCH_PRIOR|  
|AV PÁG|SQL_FETCH_NEXT|  
|Línea arriba|SQL_FETCH_RELATIVE con *FetchOffset* igual a – 1|  
|Línea abajo|SQL_FETCH_RELATIVE con *FetchOffset* igual a 1|  
|Cuadro de desplazamiento en la parte superior|SQL_FETCH_FIRST|  
|Cuadro de desplazamiento en la parte inferior|SQL_FETCH_LAST|  
|Posición del cuadro de desplazamiento aleatoria|SQL_FETCH_ABSOLUTE|  
  
 Estas aplicaciones también se deben colocar el cuadro de desplazamiento después de una operación de desplazamiento, lo que requiere el número de fila actual y el número de filas. Para el número de fila actual, las aplicaciones pueden o realizar un seguimiento del número de fila actual o llame a **SQLGetStmtAttr** con el atributo SQL_ATTR_ROW_NUMBER para recuperarlo.  
  
 El número de filas del cursor, que es el tamaño del resultado se establece, está disponible como el campo SQL_DIAG_CURSOR_ROW_COUNT del encabezado del diagnóstico. El valor de este campo está definido sólo después **SQLExecute**, **SQLExecDirect**, o **SQLMoreResult** se ha llamado. Este número puede ser un recuento aproximado o un recuento exacto, dependiendo de las capacidades del controlador. Se puede determinar la compatibilidad del controlador mediante una llamada a **SQLGetInfo** con los tipos de información de atributos de cursor y la comprobación de si el bit SQL_CA2_CRC_APPROXIMATE o SQL_CA2_CRC_EXACT se devuelve en el tipo de cursor.  
  
 Nunca se admite un recuento exacto de filas de un cursor dinámico. Para otros tipos de cursores, el controlador puede admitir recuentos de filas exacto o aproximado, pero no ambos. Si el controlador admite exacto ni aproximado recuentos de filas para un tipo de cursor específico, el campo SQL_DIAG_CURSOR_ROW_COUNT contiene el número de filas que se han capturado hasta ahora. Independientemente de qué el controlador admite, **SQLFetchScroll** con una *operación* de SQL_FETCH_LAST hará que el campo SQL_DIAG_CURSOR_ROW_COUNT contener el número exacto de filas.
