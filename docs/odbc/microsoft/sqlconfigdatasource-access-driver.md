---
title: SQLConfigDataSource (controlador de acceso) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284055"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se usa para agregar, modificar o eliminar un origen de datos utiliza dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|SECUENCIA DE INTERCALACIÓN|La secuencia en la que se ordenan los campos.<br /><br /> Esto establece la misma opción **que Secuencia de intercalación** en el cuadro de diálogo de configuración.|  
|COMPACT_DB|Realiza la compactación de datos en un archivo de base de datos. Tiene el siguiente formato: COMPACT_DB<\<path_name><optionaL_sort_order>> de palabras clave ENCRYPT opcionales.<br /><br /> Cuando se utiliza la palabra clave COMPACT_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, compactar una base de datos y especificar un DSN es un proceso de dos pasos.|  
|CREATE_DB|Crea un archivo de base de datos. Tiene el siguiente formato: CREATE_DB \<<path_name>><de orden de optional_sort optional_ENCRYPT> de palabras clave, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación será el configurado en el cuadro de diálogo Nueva base de datos que se muestra cuando se presione el botón Crear en el cuadro de diálogo Configuración de Microsoft Access. Si no se especifica ningún criterio de ordenación, se utiliza General.<br /><br /> Cuando se utiliza la palabra clave CREATE_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos. Cuando se utiliza la palabra clave CREATE_DB, si el nombre de ruta de acceso de la base de datos de Microsoft Access que se va a crear contiene uno o varios espacios, el nombre de ruta de acceso completo debe estar entre comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:-ARCHIVOS DE PROGRAMA-ARCHIVOS COMUNES- MyAccess.mdb"<br /><br /> "C:-ARCHIVOS DE PROGRAMA-Access2.mdb"<br /><br /> CREATE_DB-C:-TEMP-test.mdb (no se necesitan comillas)|  
|CREATE_SYSDB|Crea un archivo de base de datos del sistema. Tiene el siguiente formato:\<CREATE_SYSDB, \<nombre de ruta de acceso>> de orden opcional, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación será el configurado en el cuadro de diálogo **Nueva base** de datos que se muestra cuando se hace clic en el botón **Crear** en el cuadro de diálogo Configuración de ODBC **Microsoft Access.** Si no se especifica ningún criterio de ordenación, se utiliza General.|  
|CREATE_V2DB|Crea un archivo de base de datos compatible con Microsoft Access 2.0. Tiene el siguiente formato: CREATE_V2DB\< \<ruta de acceso-nombre>> de orden opcional, donde el nombre de la ruta de acceso es la ruta de acceso completa a una base de datos de Microsoft Access. Se devolverá un error si el nombre de la ruta de acceso especifica una base de datos existente. El criterio de ordenación será el configurado en el cuadro de diálogo Nueva base de datos que se muestra cuando se presione el botón Crear en el cuadro de diálogo Configuración de Microsoft Access. Si no se especifica ningún criterio de ordenación, se utiliza General.<br /><br /> Cuando se utiliza la palabra clave CREATE_V2DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, crear una base de datos y especificar un DSN es un proceso de dos pasos.<br /><br /> Cuando se utiliza la palabra clave CREATE_V2DB, si el nombre de ruta de acceso de la base de datos de Microsoft Access que se va a crear contiene uno o varios espacios, el nombre de ruta de acceso completo debe estar entre comillas dobles, como se muestra en los ejemplos siguientes:<br /><br /> "C:-ARCHIVOS DE PROGRAMA-ARCHIVOS COMUNES- MyAccess.mdb"<br /><br /> "C:-ARCHIVOS DE PROGRAMA-Access2.mdb"<br /><br /> CREATE_V2DB-C:-TEMP-test.mdb (no se necesitan comillas)|  
|DBQ|El nombre del archivo de base de datos.<br /><br /> Esto establece la misma opción que **Base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|La especificación de ruta de acceso al archivo de base de datos.|  
|DESCRIPTION|Una descripción de los datos en el origen de datos.<br /><br /> Esto establece la misma opción que **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|La especificación de ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.  25 (Microsoft Access)|  
|Fil|Tipo de archivo MS Access para Microsoft Access|  
|IMPLICITCOMMITSYNC|Determina si el controlador de Microsoft Access realizará confirmaciones internas o implícitas de forma asincrónica. Este valor se establece inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción interna/implícita.<br /><br /> El valor de esta opción no debe cambiarse sin tener en cuenta cuidadosamente las consecuencias. Para obtener más información acerca de la opción, consulte la Guía del programador de *Microsoft Jet Database Engine*.<br /><br /> Esto establece la misma opción que **ImplicitCommitSync** en el cuadro de diálogo de configuración.|  
|MAXBUFFERSIZE|El tamaño del búfer interno, en kilobytes, que utiliza Microsoft Access para transferir datos desde y hacia el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede utilizar cualquier valor entero divisible por 256. Esto establece la misma opción que **Tamaño de búfer** en el cuadro de diálogo de configuración.|  
|MAXSCANROWS|El número de filas que se analizarán al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Se puede introducir un número del 1 al 16 para que las filas se escaneen. El valor predeterminado es 8; si se establece en 0, se analizan todas las filas. (Un número fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción que **Filas para escanear** en el cuadro de diálogo de configuración.|  
|PAGETIMEOUT|Especifica el período de tiempo, en milisegundos, que una página (si no se utiliza) permanece en el búfer antes de quitarse. El valor predeterminado es cinco décimas de segundo (0,5 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción que Tiempo de espera de **página** en el cuadro de diálogo de configuración.|  
|PWD|La contraseña.|  
|READONLY|TRUE para que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de configuración.|  
|REPAIR_DB|Repara una base de datos dañada por un error que se produce durante el proceso de confirmación.<br /><br /> Cuando se utiliza la palabra clave REPAIR_DB en la misma instrucción con una palabra clave DSN, este controlador omite la palabra clave DSN. Por lo tanto, reparar una base de datos y especificar un DSN es un proceso de dos pasos.|  
|SYSTEMDB|Para el controlador de Microsoft Access, la especificación de ruta de acceso al archivo de base de datos del sistema.<br /><br /> Esto establece la misma opción que Base de **datos del sistema** en el cuadro de diálogo de configuración.|  
|Hilos|El número de subprocesos en segundo plano que va a utilizar el motor. El valor predeterminado es 3, pero se puede cambiar.<br /><br /> Esto establece la misma opción que **subprocesos** en el cuadro de diálogo de configuración.|  
|UID|Para el controlador de Microsoft Access, el nombre de ID de usuario utilizado para el inicio de sesión.|  
|USERCOMMITSYNC|Determina si el controlador de Microsoft Access realizará transacciones definidas por el usuario de forma asincrónica. Este valor se establece inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará a que se completen las confirmaciones en una transacción definida por el usuario.<br /><br /> El valor de esta opción no debe cambiarse sin tener en cuenta cuidadosamente las consecuencias. Para obtener más información acerca de la opción, consulte la Guía del programador de *Microsoft Jet Database Engine*.<br /><br /> Esto establece la misma opción que **UserCommitSync** en el cuadro de diálogo de configuración.|
