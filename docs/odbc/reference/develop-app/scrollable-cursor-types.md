---
description: Tipos de Cursor desplazable
title: Tipos de cursor desplazables | Microsoft Docs
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
ms.openlocfilehash: c27ccd54bfe0ba099d78c002fce4c901e4bf8c1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476517"
---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor desplazable
Los cuatro tipos de cursores desplazables son estáticos, dinámicos, controlados por conjunto de claves y mixtos. Los cursores estáticos detectan pocos cambios o ningún cambio, pero son relativamente baratas de implementar. Los cursores dinámicos detectan todos los cambios pero son caros de implementar. Los cursores mixtos y controlados por conjunto de claves se encuentran entre y detectan la mayoría de los cambios, pero con menos gastos que los cursores dinámicos.  
  
 Los siguientes términos se usan para definir las características de cada tipo de cursor desplazable:  
  
-   **Propias actualizaciones, eliminaciones e inserciones.** Actualizaciones, eliminaciones e inserciones realizadas a través del cursor, ya sea con una llamada a **SQLBulkOperations** o **SQLSetPos** o con una instrucción UPDATE o DELETE posicionada.  
  
-   **Otras actualizaciones, eliminaciones e inserciones.** Actualizaciones, eliminaciones e inserciones no realizadas por el cursor, incluidas las realizadas por otras operaciones en la misma transacción, las realizadas a través de otras transacciones y las realizadas por otras aplicaciones.  
  
-   **Membresía.** Conjunto de filas del conjunto de resultados.  
  
-   **Orden.** El orden en el que el cursor devuelve las filas.  
  
-   **Valor.** Los valores de cada fila del conjunto de resultados.  
  
 Para obtener información sobre cómo actualizar, eliminar e insertar datos, vea [información general](../../../odbc/reference/develop-app/updating-data-overview.md)sobre la actualización de datos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinámicos de ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de claves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mixtos](../../../odbc/reference/develop-app/mixed-cursors.md)
