---
title: Procesando instrucciones SQL | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81308006"
---
# <a name="processing-sql-statements"></a>Procesamiento de instrucciones SQL
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores ODBC pasa todas las instrucciones SQL directamente al controlador, excepto las siguientes:  
  
-   Instrucciones Update y DELETE posicionadas  
  
-   **Select for update** (instrucciones)  
  
-   Instrucciones SQL por lotes  
  
 Para ejecutar instrucciones Update y DELETE posicionadas y colocar el cursor en una fila para llamar a **SQLGetData** para esa fila, la biblioteca de cursores crea una instrucción de búsqueda que identifica la fila.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesamiento de instrucciones posicionadas Update y Delete](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [Procesamiento de instrucciones SELECT FOR UPDATE](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [Procesamiento de lotes de instrucciones SQL](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [Construcción de instrucciones Searched](../../../odbc/reference/appendixes/constructing-searched-statements.md)
