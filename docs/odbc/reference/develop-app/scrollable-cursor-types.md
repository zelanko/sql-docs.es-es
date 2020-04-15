---
title: Tipos de cursor esptables ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304236"
---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor desplazable
Los cuatro tipos de cursores desplazables son estáticos, dinámicos, controlados por conjuntos de claves y mixtos. Los cursores estáticos detectan pocos o ningún cambio, pero son relativamente baratos de implementar. Los cursores dinámicos detectan todos los cambios, pero son costosos de implementar. Los cursores mixtos y controlados por conjuntos de claves se encuentran en el medio, detectando la mayoría de los cambios, pero con menos gasto que los cursores dinámicos.  
  
 Los siguientes términos se utilizan para definir las características de cada tipo de cursor desplazable:  
  
-   **Actualizaciones, eliminaciones e inserciones propias.** Actualizaciones, eliminaciones e inserciones realizadas a través del cursor, ya sea con una llamada a **SQLBulkOperations** o **SQLSetPos** o con una instrucción de actualización o eliminación posicionada.  
  
-   **Otras actualizaciones, eliminaciones e inserciones.** Actualizaciones, eliminaciones e inserciones no realizadas por el cursor, incluidas las realizadas por otras operaciones en la misma transacción, las realizadas a través de otras transacciones y las realizadas por otras aplicaciones.  
  
-   **Membresía.** El conjunto de filas del conjunto de resultados.  
  
-   **Orden.** El orden en el que el cursor devuelve las filas.  
  
-   **Valores.** Los valores de cada fila del conjunto de resultados.  
  
 Para obtener información sobre cómo actualizar, eliminar e insertar datos, consulte Actualización de información [general de datos](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinámicos de ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de claves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mixtos](../../../odbc/reference/develop-app/mixed-cursors.md)
