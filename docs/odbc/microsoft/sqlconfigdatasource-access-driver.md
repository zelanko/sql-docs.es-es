---
title: SQLConfigDataSource (controlador de acceso) | Documentos de Microsoft
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
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24154cb8cf4f07699385f773608b929a9a4ed4a3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se utiliza para agregar, modificar o eliminar un origen de datos dinámicamente usa las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|COMPACT_DB|Realiza la compactación de datos en un archivo de base de datos. Tiene el formato siguiente: COMPACT_DB = < ruta_acceso >< optionaL_sort_order >\<palabra clave de cifrado opcional >.<br /><br /> Cuando se utiliza la palabra clave COMPACT_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, compactar una base de datos y especificando un DSN es un proceso de dos pasos.|  
|CREATE_DB|Crea un archivo de base de datos. Tiene el formato siguiente: CREATE_DB = < ruta_acceso >\<optional_sort orden >< optional_ENCRYPT palabra clave >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de ruta de acceso especifica una base de datos existente. El criterio de ordenación será como conjunto de seguridad en el cuadro de diálogo nueva base de datos cuando se presiona el botón Crear en el cuadro de diálogo de instalación de Microsoft Access. Si no se especifica ningún criterio de ordenación, se usa General.<br /><br /> Cuando se utiliza la palabra clave CREATE_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos. Cuando se usa la palabra clave CREATE_DB, si la ruta de acceso de la base de datos de Microsoft Access creará contiene uno o varios espacios, la ruta de acceso completa debe incluirse con comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\PROGRAM programa\Archivos programa\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (sin las comillas que sea necesitadas)|  
|CREATE_SYSDB|Crea un archivo de base de datos del sistema. Tiene el formato siguiente: CREATE_SYSDB =\<nombre de ruta de acceso >\<opcional de criterio de ordenación >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de ruta de acceso especifica una base de datos existente. El criterio de ordenación será como conjunto de seguridad en el **nueva base de datos** muestra el cuadro de diálogo cuando la **crear** botón se hace clic en el **ODBC Microsoft Access Setup** cuadro de diálogo. Si no se especifica ningún criterio de ordenación, se usa General.|  
|CREATE_V2DB|Crea un archivo de base de datos que sea compatible con Microsoft Access 2.0. Tiene el formato siguiente: CREATE_V2DB =\<nombre de ruta de acceso >\<opcional de criterio de ordenación >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de ruta de acceso especifica una base de datos existente. El criterio de ordenación será como conjunto de seguridad en el cuadro de diálogo nueva base de datos cuando se presiona el botón Crear en el cuadro de diálogo de instalación de Microsoft Access. Si no se especifica ningún criterio de ordenación, se usa General.<br /><br /> Cuando se utiliza la palabra clave CREATE_V2DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos.<br /><br /> Cuando se usa la palabra clave CREATE_V2DB, si la ruta de acceso de la base de datos de Microsoft Access creará contiene uno o varios espacios, la ruta de acceso completa debe incluirse con comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\PROGRAM programa\Archivos programa\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (sin las comillas que sea necesitadas)|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo de instalación.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al archivo de base de datos.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.  25 (Microsoft Access)|  
|FIL|MS Access para Microsoft Access de tipo de archivo|  
|IMPLICITCOMMITSYNC|Determina si el controlador de Microsoft Access llevará a cabo interna o implícita se confirma de forma asincrónica. Este valor está establecido inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará confirmaciones en una transacción interna o implícita se complete.<br /><br /> El valor de esta opción no debe cambiarse sin considerar atentamente las consecuencias. Para obtener más información acerca de la opción, vea el *Guía del programador del motor de base de datos Jet de Microsoft*.<br /><br /> Esto establece la misma opción como **ImplicitCommitSync** en el cuadro de diálogo de instalación.|  
|MAXBUFFERSIZE|El tamaño del búfer interno en kilobytes, que es utilizado por Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (mostrada como 2048). Puede utilizarse cualquier valor entero divisible por 256. Esto establece la misma opción como **tamaño de búfer** en el cuadro de diálogo de instalación.|  
|MAXSCANROWS|El número de filas que deben analizarse al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Un número comprendido entre 1 y 16 puede especificarse para que las filas que se va a buscar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número que está fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo de instalación.|  
|PAGETIMEOUT|Especifica el período de tiempo, en milisegundos, que una página (si no se utiliza) permanece en el búfer antes de que se va a quitar. El valor predeterminado es cinco décimas de segundo (0,5 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo de instalación.|  
|PWD|La contraseña.|  
|READONLY|TRUE para que el archivo de solo lectura; FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo de instalación.|  
|REPAIR_DB|Repara una base de datos dañado por un error que se produce durante el proceso de confirmación.<br /><br /> Cuando se utiliza la palabra clave REPAIR_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, la reparación de una base de datos y especificando un DSN es un proceso de dos pasos.|  
|SYSTEMDB|Para el controlador de Microsoft Access, la especificación de ruta de acceso al archivo de base de datos del sistema.<br /><br /> Esto establece la misma opción como **base de datos del sistema** en el cuadro de diálogo de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor predeterminado es 3, pero puede cambiarse.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo de instalación.|  
|UID|Para el controlador de Microsoft Access, usa el nombre de Id. de usuario de inicio de sesión.|  
|USERCOMMITSYNC|Determina si el controlador de Microsoft Access llevará a cabo transacciones definidas por el usuario de forma asincrónica. Este valor está establecido inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará confirmaciones en una transacción definida por el usuario se complete.<br /><br /> El valor de esta opción no debe cambiarse sin considerar atentamente las consecuencias. Para obtener más información acerca de la opción, vea el *Guía del programador del motor de base de datos Jet de Microsoft*.<br /><br /> Esto establece la misma opción como **UserCommitSync** en el cuadro de diálogo de instalación.|

