---
description: Tipos de descriptores de
title: Tipos de descriptores | Microsoft Docs
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
ms.openlocfilehash: 4ef6bcaa737e26a4a3125e980f6f6bf3c3cff070
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491350"
---
# <a name="types-of-descriptors"></a>Tipos de descriptores de
Un descriptor se utiliza para describir uno de los siguientes elementos:  
  
-   Un conjunto de cero o más parámetros. Un descriptor de parámetros se puede utilizar para describir:  
  
    -   El *búfer de parámetros de la aplicación,* que contiene los argumentos dinámicos de entrada establecidos por la aplicación o los argumentos dinámicos de salida después de la ejecución de una instrucción de **llamada** de SQL.  
  
    -   *Búfer de parámetros de implementación*. Para los argumentos dinámicos de entrada, contiene los mismos argumentos que el búfer de parámetros de la aplicación, después de cualquier conversión de datos que la aplicación pueda especificar. Para los argumentos dinámicos de salida, contiene los argumentos devueltos, antes de cualquier conversión de datos que la aplicación pueda especificar.  
  
     En el caso de los argumentos dinámicos de entrada, la aplicación debe funcionar en un descriptor de parámetro de aplicación antes de ejecutar cualquier instrucción SQL que contenga marcadores de parámetros dinámicos. En el caso de los argumentos dinámicos de entrada y salida, la aplicación puede especificar distintos tipos de datos en el descriptor de parámetros de implementación para lograr la conversión de datos.  
  
-   Una sola fila de datos de la base de datos. Se puede utilizar un descriptor de fila para describir:  
  
    -   *Búfer de filas de implementación,* que contiene la fila de la base de datos. (Estos búferes contienen datos conceptualmente según se escriben o se leen de la base de datos. Sin embargo, no se especifica la forma almacenada de los datos de la base de datos. Una base de datos puede realizar una conversión adicional en los datos de su formulario en el búfer de implementación).  
  
    -   El búfer de la fila de la *aplicación,* que contiene la fila de datos que se presenta a la aplicación, siguiendo cualquier conversión de datos que la aplicación pueda especificar.  
  
     La aplicación funciona en el descriptor de fila de la aplicación en cualquier caso en el que los datos de columna de la base de datos deben aparecer en variables de aplicación. Para lograr la conversión de datos de las columnas, la aplicación puede especificar distintos tipos de datos en el descriptor de fila de implementación.  
  
 En la tabla siguiente se resumen los tipos de descriptor.  
  
|Tipo de búfer|Filas|Parámetros dinámicos|  
|-----------------|----------|------------------------|  
|**Búfer de aplicación**|Descriptor de fila de aplicación (ARD)|Descriptor de parámetros de aplicación (APD)|  
|**Búfer de implementación**|Descriptor de fila de implementación (IRD)|Descriptor de parámetros de implementación (IPD)|  
  
 En el caso de los búferes de parámetros o de filas, si la aplicación especifica tipos de datos diferentes en los registros correspondientes de la implementación y los descriptores de la aplicación, el controlador realiza la conversión de datos cuando utiliza los descriptores. Por ejemplo, puede convertir valores numéricos y de fecha y hora en formato de cadena de caracteres. (Para las conversiones válidas, vea [Apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md)).  
  
 Un descriptor puede realizar distintos roles. Distintas instrucciones pueden compartir cualquier descriptor que la aplicación asigna explícitamente. Un descriptor de fila en una instrucción puede servir como un descriptor de parámetros en otra instrucción.  
  
 Siempre se sabe si un descriptor determinado es un descriptor de aplicación o un descriptor de implementación, incluso si el descriptor aún no se ha usado en una operación de base de datos. En el caso de los descriptores que la implementación asigna implícitamente, la implementación registra la fila predefinida relativa al identificador de instrucción. Cualquier descriptor que la aplicación asigna llamando a **SQLAllocHandle** es un descriptor de la aplicación.
