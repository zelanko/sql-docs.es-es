---
title: SQLConfigDataSource (controlador de Paradox) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b9acd359d2d99531e3fe4092b3bd20f00e94622a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se utiliza para agregar, modificar o eliminar un origen de datos dinámicamente usa las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> Cuando se utiliza el controlador de Paradox, la secuencia puede ser ASCII (valor predeterminado), internacional, sueco / finlandés o noruego danés.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo de instalación.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|EXCLUSIVO|Determina si la base de datos se abre en modo exclusivo (acceda a solo un usuario a la vez) o modo (acceda a más de un usuario a la vez) compartido. Puede ser true (modo exclusivo) o false (modo compartido).<br /><br /> Esto establece la misma opción como **exclusivo** en el cuadro de diálogo de instalación.|  
|FIL|Archivo tipo Paradox 3.x, Paradox 4.x o Paradox 5.x|  
|TIPO DE ARCHIVO|Tipo de archivo para el controlador de texto (texto).|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de que se va a quitar. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo de instalación.|  
|PARADOXNETPATH|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo PDOXUSRS.net (en Paradox 4.* x*) o el archivo PARADOX.net (en Paradox 5.* x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox creará uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Antes de que se puede seleccionar un directorio de red, debe especificarse un nombre de usuario Paradox.<br /><br /> Esto establece la misma opción como **seleccione directorio de red** en el cuadro de diálogo de instalación.|  
|PARADOXNETSTYLE|Para el controlador de Paradox, la red de acceso estilo que se va a usar al obtener acceso a datos Paradox: "3.x" para Paradox 3. *x* o "4.x" para Paradox 4.* x* ó 5.* x*. Puede establecerse en "3.x" o "4.x" si la versión es Paradox 4. *x* ó 5.* x*; si la versión es Paradox 3.* x*, el estilo debe ser "3.x".<br /><br /> Esto establece la misma opción como **estilo Net** en el cuadro de diálogo de instalación.|  
|PARADOXUSERNAME|Para el controlador de Paradox, el nombre de usuario Paradox.<br /><br /> Esto establece la misma opción como **nombre de usuario** en el cuadro de diálogo de instalación.|  
|PWD|La contraseña.<br /><br /> Esto es una palabra clave opcional y nunca se escribirán en el archivo por el controlador. Se utiliza en una llamada a **SQLDriverConnect** con archivos protegidos por contraseña de Paradox. La contraseña utilizada será válida siempre que se abre una tabla. Si no hay ninguna contraseña se pasa en la cadena de conexión, no se establece ninguna contraseña para esa tabla. Si las tablas tienen contraseñas diferentes, más de uno no se puede abrir en la misma sesión, ni pueden combinarse las tablas.|  
|READONLY|TRUE para que el archivo de solo lectura; FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo de instalación.|

