---
title: Controlador especificación subclaves | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a10a3036e049a85e44c59ad8c8fa5a09bff538be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="driver-specification-subkeys"></a>Subclaves de la especificación de controlador
Cada controlador mostrado en la subclave de controladores ODBC tiene una subclave de su propio. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave de controladores ODBC. Las rutas de acceso completas del controlador y el controlador de archivos DLL, los valores de las palabras clave de controlador devueltos por la instalación de la lista de los valores bajo esta subclave **SQLDrivers**y el recuento de uso. Los formatos de los valores son como se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**} {**Y**&AMP;#124;**N**}|  
|CreateDSN|REG_SZ|*Descripción del controlador*|  
|Controlador|REG_SZ|*ruta de DLL*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *archivo extension1*[**,\*.** *archivo extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ssNoVersion|REG_SZ|*el programa de instalación-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*Recuento*|  
  
 El uso de cada palabra clave se muestra en la tabla siguiente.  
  
|Palabra clave|Uso|  
|-------------|-----------|  
|**APILevel**|El controlador es compatible con el nivel de conformidad de interfaz de un número que indica ODBC:<br /><br /> 0 = Ninguno<br /><br /> 1 = 1 nivel compatibles<br /><br /> 2 = nivel 2 compatibles<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_ODBC_INTERFACE_CONFORMANCE en **SQLGetInfo**.|  
|**CreateDSN**|El nombre de uno o varios orígenes de datos que se crea cuando se instala el controlador. La información del sistema debe incluir una sección de especificación de origen de datos para cada origen de datos que se muestran con el **CreateDSN** palabra clave. Estas secciones no deben incluir el **controlador** (palabra clave), ya que esto se especifica en la sección de la especificación de controlador, pero debe incluir información suficiente para la **ConfigDSN** función en el controlador archivo DLL para crear una especificación de origen de datos sin mostrar los cuadros de diálogo de configuración. Para el formato de una sección de especificación del origen de datos, vea [subclaves de especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Una cadena de tres caracteres que indica si el controlador admite **SQLConnect**, **SQLDriverConnect**, y **SQLBrowseConnect**. Si el controlador admite **SQLConnect**, el primer carácter es "Y"; en caso contrario, es "N". Si el controlador admite **SQLDriverConnect**, el segundo carácter es "Y"; en caso contrario, es "N". Si el controlador admite **SQLBrowseConnect**, el tercer carácter es "Y"; en caso contrario, es "N". Por ejemplo, si un controlador es compatible con **SQLConnect** y **SQLDriverConnect** pero no **SQLBrowseConnect**, la cadena de tres caracteres es "YYN".|  
|**DriverODBCVer**|Una cadena de caracteres con la versión de ODBC que admite el controlador. La versión tiene el formato *nn.nn*, donde los dos primeros dígitos corresponden a la versión principal y los dos dígitos siguientes son la versión secundaria. Para la versión de ODBC que se describe en este manual, el controlador debe devolver "03.00".<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_DRIVER_ODBC_VER en **SQLGetInfo**.|  
|**FileExtns**|Para los controladores basados en archivos, una lista separada por comas de las extensiones de los archivos puede usar el controlador. Por ejemplo, puede especificar un controlador de dBASE \*.dbf y un controlador de archivo de texto con formato podrían especificar \*.txt,\*.csv. Para obtener un ejemplo de cómo una aplicación puede usar esta información, consulte el **FileUsage** palabra clave.|  
|**FileUsage**|Un número que indica cómo un controlador basados en archivos trata directamente los archivos en un origen de datos.<br /><br /> 0 = el controlador no es un controlador basados en archivos. Por ejemplo, un controlador ORACLE es un controlador basados en DBMS.<br /><br /> 1 = un controlador basados en archivos trata los archivos en un origen de datos como tablas. Por ejemplo, un controlador de Xbase trata cada archivo Xbase como una tabla.<br /><br /> 2 = un controlador basados en archivos trata los archivos en un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft® Access trata cada archivo de Microsoft Access como una base de datos completa.<br /><br /> Una aplicación puede utilizar esto para determinar cómo los usuarios seleccionarán los datos. Por ejemplo, los usuarios Xbase y Paradox considerar a menudo datos tal y como se almacena en archivos, mientras que los usuarios ORACLE y Microsoft Access generalmente se considera de datos tal como se almacena en tablas.<br /><br /> Cuando un usuario selecciona **abrir archivo de datos** desde el **archivo** menú, una aplicación podría mostrar el **abrir archivo de Windows** cuadro de diálogo común. La lista de tipos de archivo utilizaría las extensiones de archivo especificadas con el **FileExtns** palabra clave para controladores que especifican un **FileUsage** valor de 1 y "Y" como el segundo carácter del valor de la  **ConnectFunctions** palabra clave. Cuando el usuario selecciona un archivo, la aplicación debería llamar a **SQLDriverConnect** con el **controlador** palabra clave y, a continuación, ejecute una **seleccione \* FROM *nombre de la tabla***   instrucción.<br /><br /> Cuando el usuario selecciona **importar datos** desde el **archivo** menú, una aplicación podría mostrar una lista de descripciones de los controladores que especifican un **FileUsage** valor de 0 o 2 e "Y" como el segundo carácter del valor de la **ConnectFunctions** palabra clave. Cuando el usuario selecciona un controlador, se llamaría la aplicación **SQLDriverConnect** con el **controlador** palabra clave y, a continuación, mostrar un personalizado **Seleccionar tabla** cuadro de diálogo.|  
|**SQLLevel**|Un número que indica la gramática de SQL-92 compatible con el controlador:<br /><br /> 0 = la entrada de SQL-92<br /><br /> 1 = transitorio FIPS127-2<br /><br /> 2 = intermedio de SQL-92<br /><br /> 3 = completa de SQL-92<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_SQL_CONFORMANCE en **SQLGetInfo**.|  
  
 Para obtener información sobre recuentos de uso, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md) anteriormente en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
 Por ejemplo, supongamos que un controlador de archivos de texto con formato tiene un controlador de archivo DLL denominado Text.dll, el programa de instalación de un controlador independiente DLL denominado Txtsetup.dll y se ha instalado tres veces. Si el controlador admite el nivel de conformidad de API de nivel 1, es compatible con el nivel de conformidad de gramática mínima de SQL, trata los archivos como tablas y puede utilizar archivos con las extensiones .txt y .csv, los valores bajo la subclave de texto podrían ser el siguiente:  
  
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
