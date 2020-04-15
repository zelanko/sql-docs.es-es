---
title: Descriptores de la página de seguridad de la empresa de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305906"
---
# <a name="descriptors"></a>Descriptores de
Un identificador de descriptor hace referencia a una estructura de datos que contiene información sobre columnas o parámetros dinámicos.  
  
 Las funciones ODBC que operan en datos de columna y parámetro establecen y recuperan implícitamente campos descriptores. Por ejemplo, cuando **SQLBindCol** se llama para enlazar datos de columna, establece campos descriptores que describen completamente el enlace. Cuando **SQLColAttribute** se llama para describir los datos de columna, devuelve los datos almacenados en campos descriptores.  
  
 Una aplicación que llama a funciones ODBC no tiene por qué preocuparse por los descriptores. Ninguna operación de base de datos requiere que la aplicación obtenga acceso directo a descriptores. Sin embargo, para algunas aplicaciones, obtener acceso directo a descriptores optimiza muchas operaciones. Por ejemplo, el acceso directo a los descriptores proporciona una manera de volver a enlazar los datos de columna, que puede ser más eficaz que llamar a **SQLBindCol** de nuevo.  
  
> [!NOTE]  
>  La representación física del descriptor no está definida. Las aplicaciones obtienen acceso directo a un descriptor solo manipulando sus campos llamando a funciones ODBC con el identificador de descriptor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de descriptores de](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descriptor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Asignar y liberar los descriptores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obtener y establecer los campos de Descriptor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
