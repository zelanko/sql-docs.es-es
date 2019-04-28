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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62665347"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se usa para agregar, modificar o eliminar un origen de datos usa dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> Cuando se usa el controlador de Paradox, la secuencia puede ser ASCII (valor predeterminado), internacional, sueco / finlandés o noruego danés.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo programa de instalación.|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo programa de instalación.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo programa de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (Paradox 4.x)<br /><br /> 538 (Paradox 5.x)|  
|EXCLUSIVO|Determina si la base de datos se abrirá en modo exclusivo (obtengan acceso a solo un usuario a la vez) o modo (obtengan acceso a más de un usuario a la vez) compartido. Puede ser true (modo exclusivo) o false (modo compartido).<br /><br /> Esto establece la misma opción como **exclusivo** en el cuadro de diálogo programa de instalación.|  
|FIL|Archivo tipo Paradox 3.x, Paradox 4.x o Paradox 5.x|  
|TIPO DE ARCHIVO|Tipo de archivo para el controlador de texto (texto).|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que permanece una página (si no usa) en el búfer antes de eliminarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo programa de instalación.|  
|PARADOXNETPATH|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo PDOXUSRS.net (en 4 Paradox. *x*) o Paradox.NET (en Paradox 5. *x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox creará uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Antes de que se puede seleccionar un directorio de red, debe especificarse un nombre de usuario Paradox.<br /><br /> Esto establece la misma opción como **Seleccionar directorio de red** en el cuadro de diálogo programa de instalación.|  
|PARADOXNETSTYLE|Para el controlador de Paradox, la red acceder a estilo que se usará al obtener acceso a datos de Paradox: "3.x" para Paradox 3. *x* o "4.x" para Paradox 4. *x* o 5. *x*. Puede establecerse en "3.x" o "4.x" si la versión 4 de Paradox. *x* o 5. *x*; si la versión 3 de Paradox. *x*, el estilo debe ser "3.x".<br /><br /> Esto establece la misma opción como **estilo neto** en el cuadro de diálogo programa de instalación.|  
|PARADOXUSERNAME|Para el controlador de Paradox, el nombre de usuario Paradox.<br /><br /> Esto establece la misma opción como **nombre de usuario** en el cuadro de diálogo programa de instalación.|  
|PWD|La contraseña.<br /><br /> Esto es una palabra clave opcional y nunca se escribirán en el archivo por el controlador. Se utiliza en una llamada a **SQLDriverConnect** frente a los archivos protegidos por contraseña de Paradox. La contraseña utilizada será válida siempre que se abre una tabla. Si no se pasa ninguna contraseña en la cadena de conexión, no se establece ninguna contraseña para esa tabla. Si las tablas tienen contraseñas diferentes, más de uno no se puede abrir en la misma sesión, ni pueden combinarse las tablas.|  
|READONLY|TRUE para que el archivo de solo lectura. FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo programa de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo programa de instalación.|
