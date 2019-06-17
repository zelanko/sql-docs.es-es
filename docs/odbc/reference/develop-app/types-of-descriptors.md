---
title: Tipos de descriptores de | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a042229e3149f97b72b6e86b485771966eb80c30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305614"
---
# <a name="types-of-descriptors"></a>Tipos de descriptores de
Un descriptor se utiliza para describir uno de los siguientes:  
  
-   Un conjunto de cero o más parámetros. Un descriptor de parámetro se puede usar para describir:  
  
    -   El *búfer de parámetro de la aplicación,* que contiene cualquier los argumentos dinámicos de entrada como conjunto por la aplicación o los argumentos dinámicos de salida tras la ejecución de un **llamar** instrucción SQL.  
  
    -   El *búfer de parámetro de implementación*. Para los argumentos de entrada dinámicos, contiene los mismos argumentos que el búfer de parámetro de la aplicación después de la aplicación puede especificar cualquier conversión de datos. Para los argumentos de salida dinámicas, esto contiene los argumentos devueltos, antes de cualquier conversión de datos que puede especificar la aplicación.  
  
     Para los argumentos de entrada dinámicos, la aplicación debe funcionar en un descriptor de parámetro de la aplicación antes de ejecutar cualquier instrucción SQL que contiene marcadores de parámetros dinámicos. Para los argumentos de entrada y salidos dinámicos, la aplicación puede especificar distintos tipos de datos de los que en el descriptor de parámetro de implementación para lograr una conversión de datos.  
  
-   Una sola fila de la base de datos. Un descriptor de fila se puede usar para describir:  
  
    -   El *búferes de fila de implementación,* que contiene la fila de la base de datos. (Estos búferes conceptualmente contienen datos como se escriben en o leen desde la base de datos. Sin embargo, no se especificó el formulario almacenado de la base de datos. Una base de datos podría realizar una conversión adicional en los datos de su formulario en el búfer de la implementación.)  
  
    -   El *búfer de filas de la aplicación,* que contiene la fila de datos, tal como se presenta a la aplicación, siga cualquier conversión de datos que puede especificar la aplicación.  
  
     La aplicación funciona en el descriptor de fila de la aplicación en cualquier caso donde los datos de columna de la base de datos deben aparecer en las variables de aplicación. Para lograr la conversión de datos de la columna de datos, la aplicación puede especificar distintos tipos de datos de los que en el descriptor de fila de implementación.  
  
 En la tabla siguiente se resumen los tipos de descriptor.  
  
|Tipo de búfer|Filas|Parámetros dinámicos|  
|-----------------|----------|------------------------|  
|**Búfer de aplicación**|descriptor de fila de la aplicación (descartar)|descriptor de parámetro de aplicación (APD)|  
|**Búfer de implementación**|descriptor de fila de implementación (IRD)|descriptor de parámetro de implementación (IPD)|  
  
 Para el parámetro o los búferes de fila, si la aplicación especifica los diferentes tipos de datos en los registros correspondientes de los descriptores de implementación y aplicación, el controlador realiza la conversión de datos cuando se usan los descriptores. Por ejemplo, que puede convertir los valores numéricos y de fecha y hora en formato de cadena de caracteres. (Para conversiones válidas, vea [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Un descriptor de puede realizar distintos roles. Instrucciones diferentes pueden compartir cualquier descriptor que la aplicación se asigna explícitamente. Un descriptor de filas en una sola instrucción puede actuar como un descriptor de parámetro en otra instrucción.  
  
 Siempre se sabe si un descriptor especificado es un descriptor de aplicación o de implementación, incluso si aún no se ha usado el descriptor de una operación de base de datos. Para los descriptores de la implementación se asigna implícitamente, la implementación registra la fila predefinida en relación con el identificador de instrucción. Cualquier descriptor que asigna la aplicación mediante una llamada a **SQLAllocHandle** es un descriptor de aplicación.
