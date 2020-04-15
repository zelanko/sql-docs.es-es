---
title: Tipos de Descriptores (Tipos de Descriptores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a6c7b55194eb61c1a909ced2296e4ad2050b674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304896"
---
# <a name="types-of-descriptors"></a>Tipos de descriptores de
Un descriptor se utiliza para describir una de las siguientes opciones:  
  
-   Un conjunto de cero o más parámetros. Un descriptor de parámetrose se puede utilizar para describir:  
  
    -   El búfer de parámetros de *aplicación,* que contiene los argumentos dinámicos de entrada establecidos por la aplicación o los argumentos dinámicos de salida después de la ejecución de una instrucción **CALL** de SQL.  
  
    -   El búfer de parámetros de *implementación*. Para los argumentos dinámicos de entrada, contiene los mismos argumentos que el búfer de parámetros de aplicación, después de cualquier conversión de datos que la aplicación pueda especificar. Para los argumentos dinámicos de salida, contiene los argumentos devueltos, antes de cualquier conversión de datos que la aplicación pueda especificar.  
  
     Para los argumentos dinámicos de entrada, la aplicación debe funcionar en un descriptor de parámetro de aplicación antes de ejecutar cualquier instrucción SQL que contenga marcadores de parámetros dinámicos. Para los argumentos dinámicos de entrada y salida, la aplicación puede especificar tipos de datos diferentes de los del descriptor de parámetros de implementación para lograr la conversión de datos.  
  
-   Una sola fila de datos de base de datos. Un descriptor de fila se puede utilizar para describir:  
  
    -   El búfer de fila de *implementación,* que contiene la fila de la base de datos. (Estos búferes conceptualmente contienen datos tal como se escriben o se leen de la base de datos. Sin embargo, no se especifica la forma almacenada de datos de base de datos. Una base de datos podría realizar una conversión adicional en los datos de su formulario en el búfer de implementación.)  
  
    -   El búfer de fila de *aplicación,* que contiene la fila de datos tal como se presenta a la aplicación, después de cualquier conversión de datos que la aplicación pueda especificar.  
  
     La aplicación funciona en el descriptor de fila de la aplicación en cualquier caso donde los datos de columna de la base de datos deben aparecer en las variables de aplicación. Para lograr la conversión de datos de datos de columna, la aplicación puede especificar tipos de datos diferentes de los del descriptor de fila de implementación.  
  
 Los tipos de descriptor se resumen en la tabla siguiente.  
  
|Tipo de búfer|Filas|Parámetros dinámicos|  
|-----------------|----------|------------------------|  
|**Búfer de aplicaciones**|Descriptor de fila de aplicación (ARD)|Descriptor de parámetros de aplicación (APD)|  
|**Buffer de implementación**|Descriptor de fila de implementación (IRD)|Descriptor de parámetros de implementación (IPD)|  
  
 Para el parámetro o los búferes de fila, si la aplicación especifica diferentes tipos de datos en los registros correspondientes de los descriptores de implementación y aplicación, el controlador realiza la conversión de datos cuando utiliza los descriptores. Por ejemplo, puede convertir valores numéricos y datetime en formato de cadena de caracteres. (Para conversiones válidas, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .)  
  
 Un descriptor puede realizar diferentes roles. Diferentes instrucciones pueden compartir cualquier descriptor que la aplicación asigne explícitamente. Un descriptor de fila en una instrucción puede servir como descriptor de parámetro en otra instrucción.  
  
 Siempre se sabe si un descriptor determinado es un descriptor de aplicación o un descriptor de implementación, incluso si el descriptor aún no se ha utilizado en una operación de base de datos. Para los descriptores que la implementación asigna implícitamente, la implementación registra la fila predefinida en relación con el identificador de instrucción. Cualquier descriptor que la aplicación asigne mediante una llamada a **SQLAllocHandle** es un descriptor de aplicación.
