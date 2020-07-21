---
title: Mensajes de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305836"
---
# <a name="diagnostic-messages"></a>Mensajes de diagnóstico
Se devuelve un mensaje de diagnóstico con cada SQLSTATE. A menudo se devuelve el mismo SQLSTATE con varios mensajes diferentes. Por ejemplo, se devuelve SQLSTATE 42000 (error de sintaxis o infracción de acceso) para la mayoría de los errores en la sintaxis SQL. Sin embargo, es probable que cada error de sintaxis esté descrito por un mensaje diferente.  
  
 Los mensajes de diagnóstico de ejemplo se enumeran en la columna error de la tabla de SQLSTATEs en el Apéndice A y en cada función. Aunque los controladores pueden devolver estos mensajes, es más probable que devuelvan el mensaje que el origen de datos le pase.  
  
 Por lo general, las aplicaciones muestran mensajes de diagnóstico al usuario, junto con el código de error de SQLSTATE y nativo. Esto ayuda al usuario y al personal de soporte técnico a determinar la causa de los problemas. La información del componente incrustada en el mensaje es especialmente útil para hacerlo.  
  
 Los mensajes de diagnóstico proceden de orígenes de datos y componentes de una conexión ODBC, como controladores, puertas de enlace y el administrador de controladores. Normalmente, los orígenes de datos no son compatibles directamente con ODBC. Por consiguiente, si un componente de una conexión ODBC recibe un mensaje de un origen de datos, debe identificar el origen de datos como el origen del mensaje. También debe identificarse como el componente que recibió el mensaje.  
  
 Si el origen de un error o advertencia es un componente en sí, el mensaje de diagnóstico debe explicarlo. Por lo tanto, el texto de los mensajes tiene dos formatos diferentes. En el caso de los errores y advertencias que no se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *identificador de proveedor* **] [** *ODBC-Component-Identifier* **]** *componente: texto proporcionado*  
  
 En el caso de los errores y advertencias que se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *Vendor-Identifier* **] [** *ODBC-Component-Identifier* **] [** *Data-Source-Identifier* **]** *Data-Source* -proviened-Text  
  
 En la tabla siguiente se muestra el significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*identificador de proveedor*|Identifica el proveedor del componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente del origen de datos.|  
|*Identificador de componentes ODBC*|Identifica el componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente del origen de datos.|  
|*identificador de origen de datos*|Identifica el origen de datos. En el caso de los controladores basados en archivos, suele ser un formato de archivo, como xBase [1] para controladores basados en DBMS, este es el producto DBMS.|  
|*texto proporcionado por el componente*|Generado por el componente ODBC.|  
|*datos proporcionados por el origen de datos*|Generado por el origen de datos.|  
  
 [1] en este caso, el controlador actúa como el controlador y el origen de datos.  
  
 Los corchetes (**[]**) deben incluirse en el mensaje y no indican elementos opcionales.
