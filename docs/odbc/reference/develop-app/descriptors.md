---
title: Los descriptores de | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d50ce0c2023e187d63d08aa862398d18dc188fd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62744233"
---
# <a name="descriptors"></a>Descriptores de
Un identificador de descriptor hace referencia a una estructura de datos que contiene información acerca de las columnas o parámetros dinámicos.  
  
 Funciones ODBC que operan sobre datos de parámetro y columna implícitamente establecerán y recuperar los campos de descriptor. Por ejemplo, cuando **SQLBindCol** se llama para enlazar datos de columna, Establece los campos de descriptor que describen completamente el enlace. Cuando **SQLColAttribute** se llama para describir los datos de columna, devuelve los datos almacenados en campos de descriptor.  
  
 Una aplicación que llama a funciones ODBC no necesita preocuparse con descriptores. No hay ninguna operación de base de datos requiere que la aplicación tenga acceso directo a los descriptores. Sin embargo, algunas aplicaciones, obtengan acceso directo a los descriptores de simplifica muchas operaciones. Por ejemplo, dirigir el acceso a los descriptores de proporciona una manera de volver a enlazar datos de columna, que pueden ser más eficaces que llamar a **SQLBindCol** nuevo.  
  
> [!NOTE]  
>  No se define la representación física del descriptor. Las aplicaciones obtienen acceso directo a un descriptor de solo manipulando sus campos mediante una llamada a funciones ODBC con el identificador de descriptor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de descriptores de](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descriptor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Asignar y liberar los descriptores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obtener y establecer los campos de Descriptor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
