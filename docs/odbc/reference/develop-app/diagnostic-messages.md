---
title: Mensajes de diagnóstico | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ea827e040afa43762edc32c5a4c28de5581b94e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostic-messages"></a>Mensajes de diagnóstico
Se devuelve un mensaje de diagnóstico con cada SQLSTATE. A menudo se devuelve el mismo valor de SQLSTATE con un número de mensajes diferentes. Por ejemplo, se devuelve SQLSTATE 42000 (sintaxis o infracción de acceso) para la mayoría de los errores de sintaxis SQL. Sin embargo, los errores de sintaxis es probable que se puede describir con un mensaje diferente.  
  
 Ejemplos de mensajes de diagnóstico se muestran en la columna de Error en la tabla de SQLSTATE en el apéndice A y en cada función. Aunque los controladores pueden devolver estos mensajes, es más probables devolver el mensaje se pasa a ellos por el origen de datos.  
  
 Las aplicaciones suelen mostrar mensajes de diagnóstico para el usuario, junto con el código de error nativo y SQLSTATE. Esto ayuda al usuario y personal de soporte técnico determinar la causa de los problemas. La información de componente insertada en el mensaje es particularmente útil hacerlo.  
  
 Mensajes de diagnóstico proceden de orígenes de datos y componentes de una conexión ODBC, como los controladores y las puertas de enlace, el Administrador de controladores. Normalmente, los orígenes de datos no admiten directamente ODBC. Por lo tanto, si un componente en una conexión ODBC recibe un mensaje de un origen de datos, debe identificar el origen de datos como el origen del mensaje. También debe identificarse como el componente que recibió el mensaje.  
  
 Si el origen de un error o advertencia es un componente de sí mismo, el mensaje de diagnóstico debe explicar esto. Por lo tanto, el texto de mensajes tiene dos formatos diferentes. Para errores y advertencias que no se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *identificador de proveedor* **] [** *identificador de componente de ODBC* **]** *texto suministrado por el componente*  
  
 Para errores y advertencias que se producen en un origen de datos, el mensaje de diagnóstico debe usar este formato:  
  
 **[** *identificador de proveedor* **] [** *identificador de componente de ODBC* **] [** *identificador de origen de datos*  **]** *datos-proporcionado-texto de código fuente*  
  
 En la tabla siguiente muestra el significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*identificador de proveedor*|Identifica el proveedor del componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente desde el origen de datos.|  
|*Identificador de componente de ODBC*|Identifica el componente en el que se produjo el error o la advertencia o que recibió el error o la advertencia directamente desde el origen de datos.|  
|*identificador del origen de datos*|Identifica el origen de datos. Para los controladores basados en archivos, normalmente es un formato de archivo, como los controladores basados en DBMS para Xbase [1], éste es el producto DBMS.|  
|*texto suministrado por el componente*|Generadas por el componente ODBC.|  
|*datos de origen-proporcionado-texto*|Generado por el origen de datos.|  
  
 [1] en este caso, el controlador actúa como el controlador y el origen de datos.  
  
 Corchetes (**[]**) debe estar incluido en el mensaje y no indican elementos opcionales.
