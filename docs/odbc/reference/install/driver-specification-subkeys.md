---
title: Subclaves de especificación del controlador ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280585"
---
# <a name="driver-specification-subkeys"></a>Subclaves de la especificación del controlador
Cada controlador que aparece en la subclave Controladores ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave Controladores ODBC. Los valores de esta subclave enumeran las rutas de acceso completas de los archivos DLL de configuración del controlador y controlador, los valores de las palabras clave del controlador devueltas por **SQLDrivers**y el recuento de uso. Los formatos de los valores son los que se muestran en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|•**Y**&#124;**N**á**Y**&#124;**N**á**Y**&#124;**N**. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .|  
|CreateDSN|REG_SZ|*descripción del conductor*|  
|Controlador|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *file-extension1*[**\*, .** *archivo-extensión2*] ...|  
|Fileusage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Configurar|REG_SZ|*setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 El uso de cada palabra clave se muestra en la tabla siguiente.  
  
|Palabra clave|Uso|  
|-------------|-----------|  
|**APILevel**|Número que indica el nivel de conformidad de la interfaz ODBC admitido por el controlador:<br /><br /> 0 = Ninguno<br /><br /> 1 - Nivel 1 soportado<br /><br /> 2 - Nivel 2 soportado<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_ODBC_INTERFACE_CONFORMANCE en **SQLGetInfo**.|  
|**CreateDSN**|El nombre de uno o varios orígenes de datos que se crearán cuando se instale el controlador. La información del sistema debe incluir una sección de especificación de origen de datos para cada origen de datos que aparece con la palabra clave **CreateDSN.** Estas secciones no deben incluir la palabra clave **Driver,** ya que se especifica en la sección de especificación del controlador, pero debe incluir suficiente información para la función **ConfigDSN** en el archivo DLL de configuración del controlador para crear una especificación de origen de datos sin mostrar ningún cuadro de diálogo. Para conocer el formato de una sección de especificación de origen de datos, consulte Subclaves de [especificación](../../../odbc/reference/install/data-source-specification-subkeys.md)de origen de datos .|  
|**ConnectFunctions**|Cadena de tres caracteres que indica si el controlador admite **SQLConnect**, **SQLDriverConnect**y **SQLBrowseConnect**. Si el controlador admite **SQLConnect**, el primer carácter es "Y"; de lo contrario, es "N". Si el controlador admite **SQLDriverConnect**, el segundo carácter es "Y"; de lo contrario, es "N". Si el controlador admite **SQLBrowseConnect**, el tercer carácter es "Y"; de lo contrario, es "N". Por ejemplo, si un controlador admite **SQLConnect** y **SQLDriverConnect** pero no **SQLBrowseConnect**, la cadena de tres caracteres es "YYN".|  
|**DriverODBCVer**|Cadena de caracteres con la versión de ODBC que admite el controlador. La versión tiene el formato *nn.nn*, donde los dos primeros dígitos son la versión principal y los dos dígitos siguientes son la versión secundaria. Para la versión de ODBC que se describe en este manual, el controlador debe devolver "03.00".<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_DRIVER_ODBC_VER en **SQLGetInfo**.|  
|**FileExtns**|Para los controladores basados en archivos, una lista separada por comas de extensiones de los archivos que el controlador puede usar. Por ejemplo, un controlador \*dBASE puede especificar .dbf y \*un\*controlador de archivo de texto con formato puede especificar .txt, .csv. Para obtener un ejemplo de cómo una aplicación puede usar esta información, consulte el **FileUsage** palabra clave.|  
|**Fileusage**|Número que indica cómo un controlador basado en archivos trata directamente los archivos de un origen de datos.<br /><br /> 0 • El controlador no es un controlador basado en archivos. Por ejemplo, un controlador ORACLE es un controlador basado en DBMS.<br /><br /> 1 - Un controlador basado en archivos trata los archivos de un origen de datos como tablas. Por ejemplo, un controlador Xbase trata cada archivo Xbase como una tabla.<br /><br /> 2 - Un controlador basado en archivos trata los archivos de un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft® Access trata cada archivo de Microsoft Access como una base de datos completa.<br /><br /> Una aplicación podría usar esto para determinar cómo seleccionarán los usuarios los datos. Por ejemplo, los usuarios de Xbase y Paradox a menudo piensan en los datos almacenados en archivos, mientras que los usuarios de ORACLE y Microsoft Access generalmente piensan en los datos almacenados en tablas.<br /><br /> Cuando un usuario selecciona **Abrir archivo** de datos en el menú **Archivo,** una aplicación podría mostrar el cuadro de diálogo común Abrir archivo de **Windows.** La lista de tipos de archivo usaría las extensiones de archivo especificadas con la palabra clave **FileExtns** para los controladores que especifican un valor **FileUsage** de 1 e "Y" como segundo carácter del valor de la palabra clave **ConnectFunctions.** Después de que el usuario selecciona un archivo, la aplicación llamaría a **SQLDriverConnect** con la palabra clave **DRIVER** y, a continuación, ejecutar una instrucción **SELECT FROM \* *nombre de tabla.* **<br /><br /> Cuando el usuario selecciona **Importar datos** en el menú **Archivo,** una aplicación podría mostrar una lista de descripciones para los controladores que especifican un valor **FileUsage** de 0 o 2 y "Y" como el segundo carácter del valor de la palabra clave **ConnectFunctions.** Después de que el usuario selecciona un controlador, la aplicación llamaría a **SQLDriverConnect** con la palabra clave **DRIVER** y, a continuación, mostrar un cuadro de diálogo **seleccionar tabla** personalizado.|  
|**SQLLevel**|Un número que indica la gramática SQL-92 admitida por el controlador:<br /><br /> 0 - Entrada SQL-92<br /><br /> 1 - FIPS127-2 Transición<br /><br /> 2 - INTERMEDIO DE SQL-92<br /><br /> 3 - SQL-92 Completo<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_SQL_CONFORMANCE en **SQLGetInfo**.|  
  
 Para obtener información acerca de los recuentos de uso, consulte [Recuento](../../../odbc/reference/install/usage-counting.md) de uso sin anterioridad en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
 Por ejemplo, supongamos que un controlador para archivos de texto con formato tiene un archivo DLL de controlador denominado Text.dll, un archivo DLL de instalación de controlador independiente denominado Txtsetup.dll y se ha instalado tres veces. Si el controlador admite el nivel de conformidad de la API de nivel 1, admite el nivel de conformidad de gramática SQL mínima, trata los archivos como tablas y puede utilizar archivos con las extensiones .txt y .csv, los valores de la subclave Texto pueden ser los siguientes:  
  
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
