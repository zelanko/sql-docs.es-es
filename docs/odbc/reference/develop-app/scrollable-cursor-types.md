---
title: Tipos de Cursor desplazable | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061636"
---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor desplazable
Los cuatro tipos de cursores desplazables son estáticos, dinámicos, cursores controlados por y mixto. Los cursores estáticos detectan pocos o ningún cambio, pero son relativamente económicas implementar. Los cursores dinámicos detectan todos los cambios, pero son costosos de implementar. Cursores mixtos y controlado por encuentran entre, detectar la mayoría de los cambios, pero con un consumo menor que los cursores dinámicos.  
  
 Los siguientes términos se usan para definir las características de cada tipo de cursor desplazable:  
  
-   **Propias actualizaciones, eliminaciones e inserciones.** Las actualizaciones, eliminaciones e inserciones realizadas a través del cursor, ya sea con una llamada a **SQLBulkOperations** o **SQLSetPos** o con una posición instrucción update o delete.  
  
-   **Otros actualiza, elimina y se inserta.** Las actualizaciones, eliminaciones y las inserciones no realizadas por el cursor, las realizadas por otras operaciones en la misma transacción incluidas, aquellos realizados a través de otras transacciones y los realizados por otras aplicaciones.  
  
-   **Pertenencia.** El conjunto de filas del conjunto de resultados.  
  
-   **Orden.** El orden en que se devuelven las filas del cursor.  
  
-   **valores.** Los valores de cada fila del conjunto de resultados.  
  
 Para obtener información acerca de cómo actualizar, eliminar e insertar datos, vea [Introducción a la actualización datos](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinámicos de ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de claves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mixtos](../../../odbc/reference/develop-app/mixed-cursors.md)
