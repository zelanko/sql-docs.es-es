---
title: Subclaves de especificación de controlador | Microsoft Docs
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
ms.openlocfilehash: 8f5523c54286ed2e7cc554745dc269599115793e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094174"
---
# <a name="driver-specification-subkeys"></a>Subclaves de la especificación del controlador
Cada controlador incluido en la subclave controladores ODBC tiene una subclave propia. Esta subclave tiene el mismo nombre que el valor correspondiente en la subclave controladores ODBC. Los valores de esta subclave enumeran las rutas de acceso completas de los archivos dll de instalación del controlador y del controlador, los valores de las palabras clave del controlador devuelto por **SQLDrivers**y el recuento de uso. Los formatos de los valores son los que se muestran en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**n**} {**y**&#124;**n**}|  
|CreateDSN|REG_SZ|*controlador: Descripción*|  
|Controlador|REG_SZ|*Driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*NN. NN*|  
|FileExtns|REG_SZ|**\*.** *archivo-extension1*[**,\*.** *archivo-extension2*] ...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Instalación|REG_SZ|*Setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*contabiliza*|  
  
 En la tabla siguiente se muestra el uso de cada palabra clave.  
  
|Palabra clave|Uso|  
|-------------|-----------|  
|**APILevel**|Un número que indica el nivel de conformidad de la interfaz ODBC admitido por el controlador:<br /><br /> 0 = Ninguno<br /><br /> 1 = se admite el nivel 1<br /><br /> 2 = nivel 2 admitido<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_ODBC_INTERFACE_CONFORMANCE en **SQLGetInfo**.|  
|**CreateDSN**|Nombre de uno o más orígenes de datos que se van a crear al instalar el controlador. La información del sistema debe incluir una sección especificación de origen de datos para cada origen de datos que aparece con la palabra clave **CreateDSN** . Estas secciones no deben incluir la palabra clave **driver** , porque se especifica en la sección especificación de controladores, pero debe incluir información suficiente para la función **ConfigDSN** en el archivo dll de instalación del controlador para crear una especificación de origen de datos sin mostrar ningún cuadro de diálogo. Para obtener información sobre el formato de una especificación de origen de datos, vea [subclaves de especificación de origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Una cadena de tres caracteres que indica si el controlador admite **SQLConnect**, **SQLDriverConnect**y **SQLBrowseConnect**. Si el controlador admite **SQLConnect**, el primer carácter es "Y". de lo contrario, es "N". Si el controlador admite **SQLDriverConnect**, el segundo carácter es "Y". de lo contrario, es "N". Si el controlador admite **SQLBrowseConnect**, el tercer carácter es "Y". de lo contrario, es "N". Por ejemplo, si un controlador admite **SQLConnect** y **SQLDriverConnect** pero no **SQLBrowseConnect**, la cadena de tres caracteres es "YYN".|  
|**DriverODBCVer**|Cadena de caracteres con la versión de ODBC que admite el controlador. La versión tiene el formato *NN. NN*, donde los dos primeros dígitos son la versión principal y los dos dígitos siguientes son la versión secundaria. Para la versión de ODBC que se describe en este manual, el controlador debe devolver "03,00".<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_DRIVER_ODBC_VER en **SQLGetInfo**.|  
|**FileExtns**|En el caso de los controladores basados en archivos, es una lista separada por comas de las extensiones de los archivos que el controlador puede usar. Por ejemplo, un controlador dBASE podría especificar \*. DBF y un controlador de archivo de texto con \*formato podría especificar\*. txt,. csv. Para obtener un ejemplo de cómo una aplicación puede usar esta información, vea la palabra clave **FileUsage** .|  
|**FileUsage**|Número que indica cómo un controlador basado en archivos trata directamente los archivos de un origen de datos.<br /><br /> 0 = el controlador no es un controlador basado en archivos. Por ejemplo, un controlador de ORACLE es un controlador basado en DBMS.<br /><br /> 1 = un controlador basado en archivos trata los archivos de un origen de datos como tablas. Por ejemplo, un controlador xBase trata cada archivo xBase como una tabla.<br /><br /> 2 = un controlador basado en archivos trata los archivos de un origen de datos como un catálogo. Por ejemplo, un controlador de Microsoft® Access trata cada archivo de Microsoft Access como una base de datos completa.<br /><br /> Una aplicación podría usar esta información para determinar cómo seleccionarán los usuarios los datos. Por ejemplo, los usuarios de xBase y Paradox suelen pensar en los datos tal como se almacenan en archivos, mientras que los usuarios de ORACLE y Microsoft Access suelen pensar en los datos almacenados en las tablas.<br /><br /> Cuando un usuario selecciona **Abrir archivo de datos** en el menú **archivo** , una aplicación podría mostrar el cuadro de diálogo Abrir común de **archivos de Windows** . La lista de tipos de archivo usaría las extensiones de archivo especificadas con la palabra clave **FileExtns** para los controladores que especifican un valor **FileUsage** de 1 y "Y" como segundo carácter del valor de la palabra clave **ConnectFunctions** . Una vez que el usuario selecciona un archivo, la aplicación llamará a **SQLDriverConnect** con la palabra clave **driver** y, a continuación, ejecutará una instrucción **SELECT \* from *TABLE-Name* ** .<br /><br /> Cuando el usuario selecciona **importar datos** desde el menú **archivo** , una aplicación puede mostrar una lista de descripciones de los controladores que especifican un valor **FileUsage** de 0 o 2 y "y" como segundo carácter del valor de la palabra clave **ConnectFunctions** . Una vez que el usuario selecciona un controlador, la aplicación llamaría a **SQLDriverConnect** con la palabra clave **driver** y, a continuación, mostraría un cuadro de diálogo **seleccionar tabla** personalizada.|  
|**SQLLevel**|Un número que indica la gramática de SQL-92 admitida por el controlador:<br /><br /> 0 = entrada SQL-92<br /><br /> 1 = FIPS127-2 transición<br /><br /> 2 = SQL-92 intermedio<br /><br /> 3 = SQL-92 Full<br /><br /> Debe ser el mismo que el valor devuelto para la opción SQL_SQL_CONFORMANCE en **SQLGetInfo**.|  
  
 Para obtener información acerca de los recuentos de uso, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md) anteriormente en esta sección.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
 Por ejemplo, supongamos que un controlador para archivos de texto con formato tiene una DLL de controlador denominada text. dll, una DLL de instalación de controladores independiente denominada Txtsetup. dll y se ha instalado tres veces. Si el controlador es compatible con el nivel de conformidad de la API de nivel 1, admite el nivel mínimo de cumplimiento de la gramática de SQL, trata los archivos como tablas y puede usar archivos con las extensiones. txt y. csv, los valores de la subclave de texto pueden ser los siguientes:  
  
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
