---
title: SQLConfigDataSource (Controlador de paradoja) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283935"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se usa para agregar, modificar o eliminar un origen de datos utiliza dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|SECUENCIA DE INTERCALACIÓN|La secuencia en la que se ordenan los campos.<br /><br /> Cuando se utiliza el controlador Paradox, la secuencia puede ser ASCII (predeterminado), Internacional, sueco-finlandés o noruego-danés.<br /><br /> Esto establece la misma opción **que Secuencia de intercalación** en el cuadro de diálogo de configuración.|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción que **Base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos en el origen de datos.<br /><br /> Esto establece la misma opción que **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|La especificación de ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 26 (Paradoja 3.x)<br /><br /> 282 (Paradoja 4.x)<br /><br /> 538 (Paradoja 5.x)|  
|Exclusivo|Determina si la base de datos se abrirá en modo exclusivo (al que solo se accede un usuario a la vez) o en modo compartido (al que acceden más de un usuario a la vez). Puede ser true (modo exclusivo) o false (modo compartido).<br /><br /> Esto establece la misma opción que **Exclusivo** en el cuadro de diálogo de configuración.|  
|Fil|Tipo de archivo Paradox 3.x, Paradox 4.x o Paradox 5.x|  
|Eltipo|Tipo de archivo para el controlador de texto (texto).|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción que Tiempo de espera de **página** en el cuadro de diálogo de configuración.|  
|PARADOXNETPATH|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, porque contiene el archivo de PDOXUSRS.net (en Paradox 4.* x*) o el archivo PARADOX.net (en Paradox 5.* x*). Si el directorio no contiene uno de estos archivos, el controlador Paradox crea uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Para poder seleccionar un directorio de red, se debe introducir un nombre de usuario de Paradox.<br /><br /> Esto establece la misma opción que **Seleccionar directorio** de red en el cuadro de diálogo de configuración.|  
|PARADOXNETSTYLE|Para el controlador Paradox, el estilo de acceso a la red que se usará al acceder a los datos de Paradox: "3.x" para Paradox 3. *x* o "4.x" para Paradox 4. *x* o 5. *x*. Se puede establecer en "3.x" o "4.x" si la versión es Paradox 4. *x* o 5. *x*; si la versión es Paradox 3. *x*, el estilo debe ser "3.x".<br /><br /> Esto establece la misma opción que **Estilo de** red en el cuadro de diálogo de configuración.|  
|PARADOXUSERNAME|Para el controlador Paradox, el nombre de usuario de Paradox.<br /><br /> Esto establece la misma opción que **Nombre de usuario** en el cuadro de diálogo de configuración.|  
|PWD|La contraseña.<br /><br /> Esta es una palabra clave opcional y el controlador nunca escribirá en el archivo. Se utiliza en una llamada a **SQLDriverConnect** en archivos Paradox protegidos por contraseña. La contraseña utilizada será válida cada vez que se abra una tabla. Si no se pasa ninguna contraseña en la cadena de conexión, no se establece ninguna contraseña para esa tabla. Si las tablas tienen contraseñas diferentes, no se puede abrir más de una en la misma sesión ni se pueden unir a las tablas.|  
|READONLY|TRUE para que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de configuración.|  
|Hilos|El número de subprocesos en segundo plano que va a utilizar el motor. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que **subprocesos** en el cuadro de diálogo de configuración.|
