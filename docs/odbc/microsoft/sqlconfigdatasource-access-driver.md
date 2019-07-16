---
title: SQLConfigDataSource (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b515ed4c30d68e62a49e1044c4ddf6f5cc5ab1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985237"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se usa para agregar, modificar o eliminar un origen de datos usa dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo programa de instalación.|  
|COMPACT_DB|Realiza la compactación de datos en un archivo de base de datos. Tiene el formato siguiente: COMPACT_DB = < ruta_acceso >< optionaL_sort_order >\<palabra clave de cifrado opcional >.<br /><br /> Cuando se usa la palabra clave COMPACT_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, la compactación de una base de datos y especificando un DSN es un proceso en dos pasos.|  
|CREATE_DB|Crea un archivo de base de datos. Tiene el formato siguiente: CREATE_DB = < ruta_acceso >\<optional_sort orden >< optional_ENCRYPT palabra clave >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Si el nombre de ruta de acceso especifica una base de datos existente, se devolverá un error. El criterio de ordenación será como el conjunto de copia en el cuadro de diálogo nueva base de datos cuando se presiona el botón Crear en el cuadro de diálogo de instalación de Microsoft Access. Si no se especifica ningún criterio de ordenación, se usa General.<br /><br /> Cuando se usa la palabra clave CREATE_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso en dos pasos. Cuando se usa la palabra clave CREATE_DB, si la ruta de acceso de la base de datos de Microsoft Access a crearse contiene uno o varios espacios, a continuación, la ruta de acceso completa debe estar delimitado por comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\PROGRAM FILES\COMMON programa\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (sin comillas necesitados)|  
|CREATE_SYSDB|Crea un archivo de base de datos del sistema. Tiene el formato siguiente: CREATE_SYSDB =\<nombre de ruta de acceso >\<criterio de ordenación opcional >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Si el nombre de ruta de acceso especifica una base de datos existente, se devolverá un error. El criterio de ordenación será como el conjunto de copia en el **nueva base de datos** muestra el cuadro de diálogo cuando el **crear** hace clic en botón el **ODBC Microsoft Access Setup** cuadro de diálogo. Si no se especifica ningún criterio de ordenación, se usa General.|  
|CREATE_V2DB|Crea un archivo de base de datos que es compatible con Microsoft Access 2.0. Tiene el formato siguiente: CREATE_V2DB =\<nombre de ruta de acceso >\<criterio de ordenación opcional >, donde el nombre de ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Si el nombre de ruta de acceso especifica una base de datos existente, se devolverá un error. El criterio de ordenación será como el conjunto de copia en el cuadro de diálogo nueva base de datos cuando se presiona el botón Crear en el cuadro de diálogo de instalación de Microsoft Access. Si no se especifica ningún criterio de ordenación, se usa General.<br /><br /> Cuando se usa la palabra clave CREATE_V2DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso en dos pasos.<br /><br /> Cuando se usa la palabra clave CREATE_V2DB, si la ruta de acceso de la base de datos de Microsoft Access a crearse contiene uno o varios espacios, a continuación, la ruta de acceso completa debe estar delimitado por comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\PROGRAM FILES\COMMON programa\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (sin comillas necesitados)|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo programa de instalación.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al archivo de base de datos.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo programa de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.  25 (Microsoft Access)|  
|FIL|MS Access para Microsoft Access de tipo de archivo|  
|IMPLICITCOMMITSYNC|Determina si el controlador de Microsoft Access realizar confirmaciones internas o implícitas de forma asincrónica. Inicialmente, este valor se establece en "Sí", lo que significa que esperará el controlador de Microsoft Access para las confirmaciones en una transacción interna y implícita se complete.<br /><br /> El valor de esta opción no debe cambiarse sin consideración cuidadosa de las consecuencias. Para obtener más información acerca de la opción, vea el *Guía del programador del motor de base de datos Jet de Microsoft*.<br /><br /> Esto establece la misma opción como **ImplicitCommitSync** en el cuadro de diálogo programa de instalación.|  
|MAXBUFFERSIZE|El tamaño del búfer interno, en kilobytes, que es utilizado por Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede usar cualquier valor entero divisible por 256. Esto establece la misma opción como **tamaño de búfer** en el cuadro de diálogo programa de instalación.|  
|MAXSCANROWS|El número de filas a explorar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Un número entre 1 y 16 se puede especificar para que las filas que se va a analizar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo programa de instalación.|  
|PAGETIMEOUT|Especifica el período de tiempo, en milisegundos, que permanece una página (si no usa) en el búfer antes de eliminarse. El valor predeterminado es cinco-décimas de segundo (0,5 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo programa de instalación.|  
|PWD|La contraseña.|  
|READONLY|TRUE para que el archivo de solo lectura. FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo programa de instalación.|  
|REPAIR_DB|Repara una base de datos dañada por un error que se produce durante el proceso de confirmación.<br /><br /> Cuando se usa la palabra clave REPAIR_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, la reparación de una base de datos y especificar un DSN es un proceso de dos pasos.|  
|SYSTEMDB|Para el controlador de Microsoft Access, la especificación de ruta de acceso al archivo de base de datos del sistema.<br /><br /> Esto establece la misma opción como **base de datos del sistema** en el cuadro de diálogo programa de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor predeterminado es 3, pero puede cambiarse.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo programa de instalación.|  
|UID|Para el controlador de Microsoft Access, el nombre de Id. de usuario usado para iniciar sesión.|  
|USERCOMMITSYNC|Determina si el controlador de Microsoft Access llevará a cabo las transacciones definidas por el usuario de forma asincrónica. Inicialmente, este valor se establece en "Sí", lo que significa que esperará el controlador de Microsoft Access para las confirmaciones en una transacción definida por el usuario se complete.<br /><br /> El valor de esta opción no debe cambiarse sin consideración cuidadosa de las consecuencias. Para obtener más información acerca de la opción, vea el *Guía del programador del motor de base de datos Jet de Microsoft*.<br /><br /> Esto establece la misma opción como **UserCommitSync** en el cuadro de diálogo programa de instalación.|
