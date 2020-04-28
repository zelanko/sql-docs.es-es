---
title: Descriptores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305906"
---
# <a name="descriptors"></a>Descriptores de
Un identificador de descriptor hace referencia a una estructura de datos que contiene información sobre columnas o parámetros dinámicos.  
  
 Las funciones ODBC que operan en datos de parámetros y columnas establecen implícitamente y recuperan campos de descriptor. Por ejemplo, cuando se llama a **SQLBindCol** para enlazar datos de columna, se establecen campos de descriptor que describen completamente el enlace. Cuando se llama a **SQLColAttribute** para describir los datos de columna, devuelve los datos almacenados en los campos de descriptor.  
  
 Una aplicación que llama a funciones ODBC no tiene que preocuparse de los descriptores. Ninguna operación de base de datos requiere que la aplicación obtenga acceso directo a los descriptores. Sin embargo, para algunas aplicaciones, la obtención de acceso directo a los descriptores simplifica muchas operaciones. Por ejemplo, el acceso directo a los descriptores proporciona una manera de volver a enlazar los datos de columna, lo que puede ser más eficaz que llamar a **SQLBindCol** .  
  
> [!NOTE]  
>  No se ha definido la representación física del descriptor. Las aplicaciones obtienen acceso directo a un descriptor solo manipulando sus campos mediante una llamada a las funciones ODBC con el identificador del descriptor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de descriptores de](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descriptor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Asignar y liberar los descriptores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obtener y establecer los campos de Descriptor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
