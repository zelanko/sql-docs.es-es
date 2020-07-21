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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284055"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se utiliza para agregar, modificar o eliminar un origen de datos utiliza de forma dinámica las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Secuencia en la que se ordenan los campos.<br /><br /> Esto establece la misma opción que la **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|COMPACT_DB|Realiza la compactación de datos en un archivo de base de datos. Tiene el formato siguiente: COMPACT_DB =<path_name><optionaL_sort_order>\<palabra clave cifrada opcional>.<br /><br /> Cuando se usa la palabra clave COMPACT_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, compactar una base de datos y especificar un DSN es un proceso de dos pasos.|  
|CREATE_DB|Crea un archivo de base de datos. Tiene el siguiente formato: CREATE_DB =<path_name>\<optional_sort palabra clave><optional_ENCRYPT>, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación se establecerá en el cuadro de diálogo nueva base de datos que se muestra cuando se presiona el botón crear en el cuadro de diálogo Configuración de Microsoft Access. Si no se especifica ningún criterio de ordenación, se utiliza general.<br /><br /> Cuando se usa la palabra clave CREATE_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos. Cuando se usa la palabra clave CREATE_DB, si la ruta de acceso de la base de datos de Microsoft Access que se va a crear contiene uno o varios espacios, la ruta de acceso completa debe ir entre comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\Archivos de programa\Archivos FILEs \ acces. mdb"<br /><br /> "C:\Archivos de FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (no se necesitan comillas)|  
|CREATE_SYSDB|Crea un archivo de base de datos del sistema. Tiene el siguiente formato: CREATE_SYSDB =\<nombre-ruta de \<acceso>> de orden opcional, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación se establecerá en el cuadro de diálogo **nueva base de datos** que se muestra al hacer clic en el botón **crear** en el cuadro de diálogo **configuración de ODBC de Microsoft Access** . Si no se especifica ningún criterio de ordenación, se utiliza general.|  
|CREATE_V2DB|Crea un archivo de base de datos que es compatible con Microsoft Access 2,0. Tiene el siguiente formato: CREATE_V2DB =\<nombre-ruta de \<acceso>> de orden opcional, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación se establecerá en el cuadro de diálogo nueva base de datos que se muestra cuando se presiona el botón crear en el cuadro de diálogo Configuración de Microsoft Access. Si no se especifica ningún criterio de ordenación, se utiliza general.<br /><br /> Cuando se usa la palabra clave CREATE_V2DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos.<br /><br /> Cuando se usa la palabra clave CREATE_V2DB, si la ruta de acceso de la base de datos de Microsoft Access que se va a crear contiene uno o varios espacios, la ruta de acceso completa debe ir entre comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:\Archivos de programa\Archivos FILEs \ acces. mdb"<br /><br /> "C:\Archivos de FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (no se necesitan comillas)|  
|DBQ|Nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción que la **base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|Especificación de la ruta de acceso al archivo de base de datos.|  
|DESCRIPTION|Descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción que la **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|Especificación de la ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|IDENTIFICADOR entero para el controlador.  25 (Microsoft Access)|  
|FIL|Tipo de archivo MS Access para Microsoft Access|  
|IMPLICITCOMMITSYNC|Determina si el controlador de Microsoft Access realizará confirmaciones internas o implícitas de forma asincrónica. Este valor se establece inicialmente en "sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción interna/implícita.<br /><br /> El valor de esta opción no debe cambiarse sin tener en cuenta las consecuencias. Para obtener más información acerca de la opción, vea la *Guía del programador de Microsoft Jet motor de base de datos*.<br /><br /> Esto establece la misma opción que **ImplicitCommitSync** en el cuadro de diálogo de instalación.|  
|MAXBUFFERSIZE|Tamaño del búfer interno, en kilobytes, que utiliza Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede usar cualquier valor entero divisible por 256. Esto establece la misma opción que el **tamaño de búfer** en el cuadro de diálogo de instalación.|  
|MAXSCANROWS|Número de filas que se van a examinar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Se puede especificar un número comprendido entre 1 y 16 para las filas que se van a examinar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción que las **filas que se van a examinar** en el cuadro de diálogo de configuración.|  
|PAGETIMEOUT|Especifica el período de tiempo, en milisegundos, que una página (si no se usa) permanece en el búfer antes de quitarse. El valor predeterminado es cinco décimas de segundo (0,5 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción que el **tiempo de espera de página** en el cuadro de diálogo de instalación.|  
|PWD|La contraseña.|  
|READONLY|TRUE para hacer que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de instalación.|  
|REPAIR_DB|Repara una base de datos dañada por un error que se produce durante el proceso de confirmación.<br /><br /> Cuando se usa la palabra clave REPAIR_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, reparar una base de datos y especificar un DSN es un proceso de dos pasos.|  
|SYSTEMDB|Para el controlador de Microsoft Access, la especificación de la ruta de acceso al archivo de base de datos del sistema.<br /><br /> Esto establece la misma opción que la **base de datos del sistema** en el cuadro de diálogo de instalación.|  
|THREADPOOL|Número de subprocesos en segundo plano que va a usar el motor. El valor predeterminado es 3, pero se puede cambiar.<br /><br /> Esto establece la misma opción que los **subprocesos** en el cuadro de diálogo de instalación.|  
|UID|Para el controlador de Microsoft Access, nombre de identificador de usuario usado para el inicio de sesión.|  
|USERCOMMITSYNC|Determina si el controlador de Microsoft Access realizará las transacciones definidas por el usuario de forma asincrónica. Este valor se establece inicialmente en "sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción definida por el usuario.<br /><br /> El valor de esta opción no debe cambiarse sin tener en cuenta las consecuencias. Para obtener más información acerca de la opción, vea la *Guía del programador de Microsoft Jet motor de base de datos*.<br /><br /> Esto establece la misma opción que **UserCommitSync** en el cuadro de diálogo de instalación.|
