---
title: "Introducción a SSMA para Sybase consola (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 239b7a8f4dbc3069e67d680b319bf426a0f917e6
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-console-sybasetosql"></a>Introducción a SSMA para Sybase consola (SybaseToSQL)
Esta sección describe el procedimiento para iniciar y empezar a trabajar con la aplicación de consola de Sybase. También se muestran en este documento, se utilizan las convenciones en una ventana de salida de consola SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar la consola SSMA  
Utilice los pasos siguientes para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a inicio y seleccione todos los programas.  
  
2.  Haga clic en el **SQL Server Migration Assistant para Sybase símbolo del sistema** acceso directo.  
  
    Muestra el menú de uso de la consola de SSMA y `(/? Help)`, que le ayudarán a empezar a trabajar con la aplicación de consola.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimiento para usar la consola SSMA  
Después de la consola se inicia correctamente en el sistema de Windows, podría utilizar los pasos siguientes para trabajar con ella:  
  
1.  Configurar la consola SSMA a través de los archivos de script. Para obtener más información acerca de esta sección, vea [crear archivos de Script &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md) .  
  
2.  [Crear archivos de valor de la Variable &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Crear los archivos de conexión de servidor &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Ejecutar la consola SSMA &#40; SybaseToSQL &#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) según sus necesidades de proyecto  
  
Características adicionales:  
  
1.  [Especifique una contraseña](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) y exportar / importar en otros equipos de la ventana  
  
2.  [Generar informes](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) ver el xml detallado informes de evaluación /conversion y migración de datos de salida. También se pueden generar informes de errores detallada para comandos de actualización y la sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de salida de consola SSMA  
Al ejecutar los comandos de script SSMA y opciones, el programa de consola muestra los resultados y mensajes (información, error, etc.) para el usuario en la consola o si es necesario, se redirige a un archivo de salida xml. Cada tipo de mensaje en la salida se especifica mediante un color único. Por ejemplo, el mensaje de texto en color blanco denota secuencias de comandos de archivo; uno de color verde representa un símbolo del sistema de entrada del usuario y así sucesivamente.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Interpretación de color de la salida de la consola en la tabla siguiente:  
  
|Color|Description|  
|---------|---------------|  
|Rojo|Error irrecuperable durante la ejecución|  
|Gris|Marca de fecha y hora, el mensaje al usuario|  
|Blanco|Comandos del archivo de script, tipo de mensaje|  
|Amarillo|Advertencia|  
|Verde|Símbolo del sistema de entrada del usuario|  
|Cian|Iniciar, finalizar y el resultado de una operación|  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
  

