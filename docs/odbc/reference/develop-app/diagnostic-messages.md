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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39ebda5de5820cdfd7333ad1d0997593922e0a4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039893"
---
# <a name="diagnostic-messages"></a>Mensajes de diagnóstico
Con cada SQLSTATE, se devuelve un mensaje de diagnóstico. A menudo se devuelve el mismo valor de SQLSTATE con un número de mensajes diferentes. Por ejemplo, se devuelve SQLSTATE 42000 (sintaxis o infracción de acceso) para la mayoría de los errores de sintaxis SQL. Sin embargo, cada error de sintaxis es probable que describirse mediante un mensaje diferente.  
  
 Ejemplos de mensajes de diagnóstico se muestran en la columna de Error en la tabla de SQLSTATE en el apéndice A y en cada función. Aunque los controladores pueden devolver estos mensajes, están más probables que devuelva el mensaje se pasa a ellos por el origen de datos.  
  
 Generalmente, las aplicaciones mostrar mensajes de diagnóstico al usuario, junto con SQLSTATE y código de error nativo. Esto ayuda al usuario y personal de soporte técnico determinar la causa de los problemas. La información del componente incrustada en el mensaje es especialmente útil para hacer esto.  
  
 Mensajes de diagnóstico proceden de orígenes de datos y los componentes de una conexión ODBC, como controladores, las puertas de enlace y el Administrador de controladores. Normalmente, los orígenes de datos no admiten directamente ODBC. Por lo tanto, si un componente en una conexión ODBC recibe un mensaje desde un origen de datos, debe identificar el origen de datos como el origen del mensaje. También debe identificarse como el componente que recibió el mensaje.  
  
 Si el origen de un error o advertencia es un componente en Sí, el mensaje de diagnóstico debe explicar esto. Por lo tanto, el texto de mensajes tiene dos formatos diferentes. Para errores y advertencias que no se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **]** *component-supplied-text*  
  
 Para errores y advertencias que se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **][** *data-source-identifier* **]** *data-source-supplied-text*  
  
 En la tabla siguiente se muestra el significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*vendor-identifier*|Identifica el proveedor del componente en el que se produjo el error o advertencia, o que recibió el error o advertencia directamente desde el origen de datos.|  
|*ODBC-component-identifier*|Identifica el componente en el que se produjo el error o advertencia, o que recibió el error o advertencia directamente desde el origen de datos.|  
|*data-source-identifier*|Identifica el origen de datos. Para los controladores basados en archivos, esto normalmente es un formato de archivo, como los controladores basados en DBMS de Xbase [1], este es el producto DBMS.|  
|*component-supplied-text*|Generado por el componente ODBC.|  
|*data-source-supplied-text*|Generado por el origen de datos.|  
  
 [1] en este caso, el controlador actúa como el controlador y el origen de datos.  
  
 Corchetes ( **[]** ) debe estar incluido en el mensaje y no indican elementos opcionales.
