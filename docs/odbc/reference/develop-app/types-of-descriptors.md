---
title: Tipos de descriptores de | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5554b0d7d110db9270230c25ab2bcc29d5a7cb87
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-descriptors"></a>Tipos de descriptores de
Un descriptor de se utiliza para describir uno de los siguientes:  
  
-   Un conjunto de cero o más parámetros. Un descriptor de parámetro se puede utilizar para describir:  
  
    -   El *búfer de parámetros de la aplicación,* que contiene cualquier los argumentos dinámicos de entrada como conjunto por la aplicación o los argumentos de salida dinámica después de la ejecución de un **llamar** instrucción de SQL.  
  
    -   El *búfer de parámetros de implementación*. Para argumentos de entrada dinámicos, contiene los mismos argumentos que el búfer de parámetro de la aplicación después de la aplicación puede especificar cualquier conversión de datos. Para los argumentos de salida dinámicos, esto contiene los argumentos devueltos, antes de cualquier conversión de datos que puede especificar la aplicación.  
  
     Para argumentos de entrada dinámicos, la aplicación debe funcionar en un descriptor de parámetro de la aplicación antes de ejecutar cualquier instrucción SQL que contiene marcadores de parámetros dinámicos. Para los argumentos dinámicos de entrada y salidos, la aplicación puede especificar tipos de datos diferentes de los del descriptor de parámetro de implementación para lograr la conversión de datos.  
  
-   Una sola fila de la base de datos. Un descriptor de fila puede utilizarse para describir:  
  
    -   El *búfer de filas de implementación,* que contiene la fila de la base de datos. (Estos búferes conceptualmente contienen datos tal y como se escriben en o leen desde la base de datos. Sin embargo, no se especifica el formato almacenado de la base de datos. Una base de datos podría realizar una conversión adicional de los datos de su formulario en el búfer de implementación.)  
  
    -   El *búfer de filas de aplicación,* que contiene la fila de datos tal como se presenta a la aplicación, después de cualquier conversión de datos que puede especificar la aplicación.  
  
     La aplicación trabaja en el descriptor de fila de la aplicación en cualquier caso donde los datos de columna de la base de datos deben aparecer en las variables de aplicación. Para lograr una conversión de datos de columna de datos, la aplicación puede especificar distintos tipos de datos de los en el descriptor de fila de implementación.  
  
 Los tipos de descriptor se resumen en la tabla siguiente.  
  
|Tipo de búfer|Filas|Parámetros dinámicos|  
|-----------------|----------|------------------------|  
|**Búfer de aplicación**|Descriptor de fila de la aplicación (descartar)|Descriptor de parámetro de aplicación (APD)|  
|**Búfer de implementación**|Descriptor de fila de implementación (IRD)|Descriptor de parámetro de implementación (IPD)|  
  
 Para el parámetro o los búferes de fila, si la aplicación especifica distintos tipos de datos en los registros correspondientes de los descriptores de implementación y aplicación, el controlador realiza la conversión de datos cuando utiliza los descriptores. Por ejemplo, pueden convertir valores numéricos y de fecha y hora en formato de cadena de caracteres. (Para las conversiones válidas, vea [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Un descriptor de puede realizar distintas funciones. Instrucciones diferentes pueden compartir cualquier descriptor de la aplicación se asigna explícitamente. Un descriptor de fila en una sola instrucción puede actuar como un descriptor de parámetro en otra instrucción.  
  
 Siempre se sabe si un descriptor determinado es un descriptor de la aplicación o un descriptor de implementación, incluso si el descriptor aún no se ha usado en una operación de base de datos. Para los descriptores de la implementación se asigna implícitamente, la implementación registra la fila predefinida en relación con el identificador de instrucción. Cualquier descriptor que asigna la aplicación mediante una llamada a **SQLAllocHandle** es un descriptor de la aplicación.

