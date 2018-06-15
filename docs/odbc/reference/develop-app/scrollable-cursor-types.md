---
title: Tipos de Cursor desplazable | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54acbd1010d546649b1ad92a34289fa4d04da162
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912420"
---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor desplazable
Los cuatro tipos de cursores desplazables son estáticos, dinámicos, cursores controlados por y mixto. Los cursores estáticos detectan pocos o ningún cambio pero son relativamente baratos implementar. Los cursores dinámicos detectan todos los cambios, pero son caros de implementar. Los cursores controlados por conjunto de claves y mixtos se encuentran entre los dos anteriores, pero con un consumo menor que los cursores dinámicos.  
  
 Los siguientes términos se utilizan para definir las características de cada tipo de cursor desplazable:  
  
-   **Propias actualizaciones, eliminaciones e inserciones.** Las actualizaciones, eliminaciones e inserciones realizadas a través del cursor, ya sea con una llamada a **SQLBulkOperations** o **SQLSetPos** o con una posición instrucción update o delete.  
  
-   **Otros actualizaciones, se elimina y se inserta.** Las actualizaciones, eliminaciones y las inserciones que no realizadas el cursor, las realizadas por otras operaciones en la misma transacción incluidas, las realizadas por otras transacciones y las realizadas por otras aplicaciones.  
  
-   **Miembro del grupo.** El conjunto de filas del conjunto de resultados.  
  
-   **Orden.** El orden en que se devuelven filas por el cursor.  
  
-   **valores.** Los valores de cada fila del conjunto de resultados.  
  
 Para obtener información acerca de cómo actualizar, eliminar e insertar datos, vea [Introducción a datos de la actualización](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinámicos de ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de claves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mixtos](../../../odbc/reference/develop-app/mixed-cursors.md)
