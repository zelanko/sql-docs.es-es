---
title: SQLConfigDataSource (controlador de Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e60d7ca9c37865c1b265297d24591638a44965
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283935"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se utiliza para agregar, modificar o eliminar un origen de datos utiliza de forma dinámica las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Secuencia en la que se ordenan los campos.<br /><br /> Cuando se usa el controlador de Paradox, la secuencia puede ser ASCII (valor predeterminado), internacional, Sueco-Finés o noruego-danés.<br /><br /> Esto establece la misma opción que la **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|DBQ|Nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción que la **base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|Especificación de la ruta de acceso al directorio.|  
|DESCRIPTION|Descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción que la **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|Especificación de la ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|IDENTIFICADOR entero para el controlador.<br /><br /> 26 (Paradox 3. x)<br /><br /> 282 (Paradox 4. x)<br /><br /> 538 (Paradox 5. x)|  
|ÚNICO|Determina si la base de datos se abrirá en modo exclusivo (a la que accede solo un usuario a la vez) o el modo compartido (al que tiene acceso más de un usuario a la vez). Puede ser true (modo exclusivo) o false (modo compartido).<br /><br /> Esto establece la misma opción que **exclusiva** en el cuadro de diálogo de instalación.|  
|FIL|Tipo de archivo Paradox 3. x, Paradox 4. x o Paradox 5. x|  
|FILETYPE|Tipo de archivo del controlador de texto (texto).|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se usa) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción que el **tiempo de espera de página** en el cuadro de diálogo de instalación.|  
|PARADOXNETPATH|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo PDOXUSRS.net (en Paradox 4.* x*) o el archivo Paradox.net (en Paradox 5.* x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox crea uno. Para obtener información acerca de estos archivos, vea la documentación de Paradox.<br /><br /> Antes de que se pueda seleccionar un directorio de red, debe especificarse un nombre de usuario de Paradox.<br /><br /> Esto establece la misma opción que **seleccionar directorio de red** en el cuadro de diálogo de instalación.|  
|PARADOXNETSTYLE|Para el controlador de Paradox, el estilo de acceso a la red que se va a usar al obtener acceso a los datos de Paradox: "3. x" para Paradox 3. *x* o "4. x" para Paradox 4. *x* o 5. *x*. Se puede establecer en "3. x" o "4. x" si la versión es Paradox 4. *x* o 5. *x*; Si la versión es Paradox 3. *x*, el estilo debe ser "3. x".<br /><br /> Esto establece la misma opción que el **estilo net** en el cuadro de diálogo de instalación.|  
|PARADOXUSERNAME|Para el controlador de Paradox, el nombre de usuario de Paradox.<br /><br /> Esto establece la misma opción que el **nombre de usuario** en el cuadro de diálogo de instalación.|  
|PWD|La contraseña.<br /><br /> Esta es una palabra clave opcional y el controlador nunca lo escribirá en el archivo. Se utiliza en una llamada a **SQLDriverConnect** contra archivos de Paradox protegidos con contraseña. La contraseña utilizada será válida cada vez que se abra una tabla. Si no se pasa ninguna contraseña en la cadena de conexión, no se establece ninguna contraseña para esa tabla. Si las tablas tienen contraseñas diferentes, no se puede abrir más de una en la misma sesión, ni se pueden combinar las tablas.|  
|READONLY|TRUE para hacer que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de instalación.|  
|THREADPOOL|Número de subprocesos en segundo plano que va a usar el motor. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que los **subprocesos** en el cuadro de diálogo de instalación.|
