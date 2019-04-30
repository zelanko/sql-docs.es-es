---
title: Subclaves de la especificación de controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b15aa278e2fe38afe93f5628433a6c8f4b41cd8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198318"
---
# <a name="driver-specification-subkeys"></a>Subclaves de la especificación del controlador
Cada controlador mostrado en la subclave de controladores ODBC tiene una subclave de su propio. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave de controladores ODBC. Las rutas de acceso completas del controlador y el controlador de archivos DLL, los valores de las palabras clave de controlador devueltos por la instalación de la lista de los valores bajo esta subclave **SQLDrivers**y el recuento de uso. Los formatos de los valores son como se muestra en la tabla siguiente.  
  
|Name|Tipo de datos|Datos|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*driver-description*|  
|Controlador|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *archivo extension1*[**,\*.** *archivo extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Programa de instalación|REG_SZ|*setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*Recuento*|  
  
 El uso de cada palabra clave se muestra en la tabla siguiente.  
  
|Palabra clave|Uso|  
|-------------|-----------|  
|**APILevel**|Un número que indica ODBC compatible con el controlador de nivel de conformidad con la interfaz:<br /><br /> 0 = Ninguno<br /><br /> 1 = 1 nivel compatibles<br /><br /> 2 = nivel 2 admitidas<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_ODBC_INTERFACE_CONFORMANCE en **SQLGetInfo**.|  
|**CreateDSN**|El nombre de uno o varios orígenes de datos cuando el controlador está instalado. La información del sistema debe incluir una sección de especificación de origen de datos para cada origen de datos que se muestran con el **CreateDSN** palabra clave. Estas secciones no deben incluir el **controlador** palabra clave, ya que esto se especifica en la sección de la especificación de controlador, pero debe incluir información suficiente para que el **ConfigDSN** función en el controlador archivo DLL para crear una especificación de origen de datos sin mostrar ningún cuadro de diálogo de configuración. Para el formato de una sección de especificación del origen de datos, vea [subclaves de especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Una cadena de tres caracteres que indica si el controlador admite **SQLConnect**, **SQLDriverConnect**, y **SQLBrowseConnect**. Si el controlador admite **SQLConnect**, el primer carácter es "Y"; en caso contrario, es "N". Si el controlador admite **SQLDriverConnect**, el segundo carácter es "Y"; en caso contrario, es "N". Si el controlador admite **SQLBrowseConnect**, el tercer carácter es "Y"; en caso contrario, es "N". Por ejemplo, si un controlador es compatible con **SQLConnect** y **SQLDriverConnect** pero no **SQLBrowseConnect**, la cadena de tres caracteres es "YYN".|  
|**DriverODBCVer**|Una cadena de caracteres con la versión de ODBC que admite el controlador. Es la versión del formulario *nn.nn*, donde los dos primeros dígitos son la versión principal y los dos dígitos son la versión secundaria. Para la versión de ODBC que se describe en este manual, el controlador debe devolver "03.00".<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_DRIVER_ODBC_VER en **SQLGetInfo**.|  
|**FileExtns**|Para los controladores basados en archivos, una lista separada por comas de extensiones de los archivos puede usar el controlador. Por ejemplo, podría especificar un controlador de dBASE \*.dbf y un controlador de archivo de texto con formato podrían especificar \*.txt,\*.csv. Para obtener un ejemplo de cómo una aplicación puede utilizar esta información, consulte el **FileUsage** palabra clave.|  
|**FileUsage**|Un número que indica el modo en que un controlador basado en archivos trata directamente los archivos en un origen de datos.<br /><br /> 0 = el controlador no es un controlador basado en archivos. Por ejemplo, un controlador ORACLE es un controlador basados en DBMS.<br /><br /> 1 = un controlador basado en archivos trata los archivos en un origen de datos como tablas. Por ejemplo, un controlador de Xbase trata cada archivo Xbase como una tabla.<br /><br /> 2 = un controlador basado en archivos trata los archivos en un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft® Access trata cada archivo de Microsoft Access como una base de datos completa.<br /><br /> Una aplicación puede utilizar esto para determinar cómo seleccionarán los usuarios los datos. Por ejemplo, los usuarios de Xbase y Paradox suelen pensar de datos tal como se almacena en archivos, mientras que los usuarios ORACLE y Microsoft Access generalmente se considera datos tal como se almacena en tablas.<br /><br /> Cuando un usuario selecciona **abrir archivo de datos** desde el **archivo** menú, una aplicación podría mostrar el **Windows File Open** cuadro de diálogo común. La lista de tipos de archivo utilizaría las extensiones de archivo especificadas con el **FileExtns** palabra clave para los controladores que especifican un **FileUsage** valor 1 y "Y" como el segundo carácter del valor de la  **ConnectFunctions** palabra clave. Después de que el usuario selecciona un archivo, se llamaría la aplicación **SQLDriverConnect** con el **controlador** palabra clave y, a continuación, ejecute un **seleccione \* FROM *nombre de tabla***   instrucción.<br /><br /> Cuando el usuario selecciona **importar datos** desde el **archivo** menú, una aplicación podría mostrar una lista de descripciones de los controladores que especifican un **FileUsage** el valor de 0 o 2 y "S" como el segundo carácter del valor de la **ConnectFunctions** palabra clave. Después de que el usuario selecciona un controlador, se llamaría la aplicación **SQLDriverConnect** con el **controlador** palabra clave y, después, mostrar un personalizado **Seleccionar tabla** cuadro de diálogo.|  
|**SQLLevel**|Un número que indica el controlador admitida la gramática de SQL-92:<br /><br /> 0 = la entrada de SQL-92<br /><br /> 1 = transitorias FIPS127-2<br /><br /> 2 = intermedio SQL-92<br /><br /> 3 = completo de SQL-92<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_SQL_CONFORMANCE en **SQLGetInfo**.|  
  
 Para obtener información sobre recuentos de uso, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md) anteriormente en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
 Por ejemplo, supongamos que un controlador de archivos de texto con formato tiene un controlador de archivo DLL denominado Text.dll, un programa de instalación de controlador independiente DLL denominado Txtsetup.dll y se ha instalado los tres veces. Si el controlador admite el nivel de conformidad de la API de nivel 1, es compatible con el nivel de conformidad de gramática mínima de SQL, trata los archivos como tablas y puede utilizar archivos con las extensiones .txt y. csv, los valores bajo la subclave texto podrían ser como sigue:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
