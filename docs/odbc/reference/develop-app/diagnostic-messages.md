---
title: Mensajes de diagnóstico ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305836"
---
# <a name="diagnostic-messages"></a>Mensajes de diagnóstico
Se devuelve un mensaje de diagnóstico con cada SQLSTATE. El mismo SQLSTATE se devuelve a menudo con un número de mensajes diferentes. Por ejemplo, SQLSTATE 42000 (error de sintaxis o infracción de acceso) se devuelve para la mayoría de los errores en la sintaxis SQL. Sin embargo, es probable que cada error de sintaxis se describa mediante un mensaje diferente.  
  
 Los mensajes de diagnóstico de ejemplo se enumeran en la columna Error de la tabla de SQLSTATEs del Apéndice A y en cada función. Aunque los controladores pueden devolver estos mensajes, es más probable que devuelvan cualquier mensaje que les pase el origen de datos.  
  
 Las aplicaciones suelen mostrar mensajes de diagnóstico al usuario, junto con el código de error SQLSTATE y nativo. Esto ayuda al usuario y al personal de soporte a determinar la causa de cualquier problema. La información del componente incrustada en el mensaje es especialmente útil para hacerlo.  
  
 Los mensajes de diagnóstico proceden de orígenes de datos y componentes de una conexión ODBC, como controladores, puertas de enlace y el Administrador de controladores. Normalmente, los orígenes de datos no admiten directamente ODBC. Por lo tanto, si un componente de una conexión ODBC recibe un mensaje de un origen de datos, debe identificar el origen de datos como el origen del mensaje. También debe identificarse como el componente que recibió el mensaje.  
  
 Si el origen de un error o advertencia es un componente en sí, el mensaje de diagnóstico debe explicar esto. Por lo tanto, el texto de los mensajes tiene dos formatos diferentes. Para errores y advertencias que no se producen en un origen de datos, el mensaje de diagnóstico debe utilizar este formato:  
  
 **[** *identificador de proveedor* **][** IDENTIFICADOR de componente ODBC ] *componente-identificador-módulo ] componente-identificador-texto suministrado* *ODBC-component-identifier* **]**  
  
 Para los errores y advertencias que se producen en un origen de datos, el mensaje de diagnóstico debe utilizar este formato:  
  
 **[** *identificador de proveedor* **][** *ODBC-component-identifier* **][** *data-source-identifier ] data-source-supplied-text* **]** *data-source-supplied-text*  
  
 En la tabla siguiente se muestra el significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*identificador de proveedor*|Identifica el proveedor del componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente del origen de datos.|  
|*ODBC-componente-identificador*|Identifica el componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente del origen de datos.|  
|*identificador de fuente de datos*|Identifica el origen de datos. Para los controladores basados en archivos, este suele ser un formato de archivo, como Xbase[1] Para los controladores basados en DBMS, este es el producto DBMS.|  
|*texto suministrado por componentes*|Generado por el componente ODBC.|  
|*data-source-supplied-text*|Generado por el origen de datos.|  
  
 [1] En este caso, el controlador actúa como el controlador y la fuente de datos.  
  
 Los corchetes (**[ ]**) deben incluirse en el mensaje y no indican elementos opcionales.
