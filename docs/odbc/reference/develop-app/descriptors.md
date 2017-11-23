---
title: Descriptores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f9a2016a57c9c2b9d105761c65be14809fee8798
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="descriptors"></a>Descriptores de
Un identificador de descriptor hace referencia a una estructura de datos que contiene información sobre las columnas o parámetros dinámicos.  
  
 Funciones ODBC que operan sobre datos de parámetro y columna implícitamente establecerán y recuperar los campos de descriptor. Por ejemplo, cuando **SQLBindCol** se llama para enlazar datos de la columna, Establece los campos de descriptor que describen completamente el enlace. Cuando **SQLColAttribute** se llama para describir los datos de la columna, devuelve los datos almacenados en campos de descriptor.  
  
 Una aplicación que llama a funciones ODBC no necesita preocuparse por descriptores. No hay ninguna operación de base de datos requiere que la aplicación tenga acceso directo a descriptores. Sin embargo, en algunas aplicaciones, acceder directamente a descriptores simplifica muchas operaciones. Por ejemplo, dirigir el acceso a los descriptores de proporciona una manera de cambiar el enlace de datos de columna, que pueden ser más eficaces que llamar a **SQLBindCol** nuevo.  
  
> [!NOTE]  
>  No se define la representación física del descriptor. Las aplicaciones tenga acceso directo a un descriptor solo mediante la manipulación de sus campos mediante una llamada a funciones ODBC con el identificador de descriptor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de descriptores de](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descriptor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Asignar y liberar los descriptores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obtener y establecer los campos de Descriptor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
