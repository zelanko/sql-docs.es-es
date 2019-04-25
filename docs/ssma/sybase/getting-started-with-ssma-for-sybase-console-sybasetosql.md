---
title: Introducción a SSMA para Sybase consola (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 608457b1732d2c1cc188b4b419903d20faa642c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631963"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Introducción a SSMA para Sybase consola (SybaseToSQL)
En esta sección se describe el procedimiento para iniciar e Introducción a SSMA para Sybase aplicación de consola. También se enumeran en este documento se utilizan las convenciones en una ventana de salida de la consola SSMA típica.  
  
## <a name="launching-the-ssma-console"></a>Iniciar la consola de SSMA  
Use los pasos siguientes para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a inicio y, a continuación, seleccione todos los programas.  
  
2.  Haga clic en el **SQL Server Migration Assistant para Sybase símbolo del sistema** acceso directo.  
  
    Muestra el menú de uso de la consola SSMA y `(/? Help)`, que le ayudarán a empezar a trabajar con la aplicación de consola.  
  
## <a name="using-the-ssma-console"></a>Mediante la consola de SSMA  
Después de la consola se inicia correctamente en el sistema de Windows, puede usar los pasos siguientes para trabajar en ella:  
  
1.  Configure la consola SSMA a través de los archivos de script. Para obtener más información en esta sección, consulte [crear archivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Creación de archivos de valor Variable &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Creación de los archivos de conexión de servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Ejecución de la consola de SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) según las necesidades del proyecto. 
  
Características adicionales:  
  
1.  [Especifique una contraseña](managing-passwords-sybasetosql.md) y la exportación e importación, en otros equipos de la ventana.  
  
2.  [Generar informes](generating-reports-sybasetosql.md) ver el xml detallado de salida de informes de evaluación/conversión y migración de datos. También puede generar informes de errores detallada para los comandos de actualización y la sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de la salida de la consola SSMA  
Al ejecutar los comandos de script SSMA y opciones, el programa de consola muestra los resultados y mensajes (información, error, etc.) al usuario en la consola o bien, si es necesario, se redirige a un archivo de salida xml. Cada tipo de mensaje en la salida se especifica mediante un color único. Por ejemplo, el mensaje de texto en color blanco indica los comandos del archivo de script; el que aparece en color verde representa un símbolo del sistema de entrada del usuario y así sucesivamente.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Interpretación de color de la salida de la consola aparece en la tabla siguiente:  
  
|Color|Descripción|  
|---------|---------------|  
|Rojo|Error irrecuperable durante la ejecución|  
|Gris|Marca de fecha y hora, el mensaje al usuario|  
|Blanco|Secuencias de comandos del archivo, tipo de mensaje|  
|Amarillo|Advertencia|  
|Verde|Símbolo del sistema de entrada del usuario|  
|Cian|Inicio, finalización y el resultado de una operación|  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
