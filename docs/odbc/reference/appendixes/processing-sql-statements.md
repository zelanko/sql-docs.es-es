---
title: Procesamiento de instrucciones SQL ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eda640f6e810eeccbfa17ea2b6ba7c1b19b28e08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308006"
---
# <a name="processing-sql-statements"></a>Procesamiento de instrucciones SQL
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores ODBC pasa todas las instrucciones SQL directamente al controlador, excepto lo siguiente:  
  
-   Instrucciones de actualización y eliminación posicionadas  
  
-   **SELECT FOR UPDATE** statements  
  
-   Instrucciones SQL por lotes  
  
 Para ejecutar instrucciones de actualización y eliminación posicionadas y para colocar el cursor en una fila para llamar a **SQLGetData** para esa fila, la biblioteca de cursores construye una instrucción buscada que identifica la fila.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesamiento de instrucciones posicionadas Update y Delete](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Procesamiento de instrucciones SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Procesamiento de lotes de instrucciones SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Construcción de instrucciones Searched](../../../odbc/reference/appendixes/constructing-searched-statements.md)
