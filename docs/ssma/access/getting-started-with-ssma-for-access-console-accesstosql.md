---
title: "Introducción a SSMA para la consola de acceso (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
caps.latest.revision: "21"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c8fff49c85afde0b576f6d4469bde5ce426171e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Introducción a SSMA para la consola de acceso (AccessToSQL)
Esta sección describe el procedimiento para iniciar y empezar a trabajar con la aplicación de consola de acceso. También se muestran en este documento, se utilizan las convenciones en una ventana de salida de consola SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar la consola SSMA  
Utilice los pasos siguientes para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a **iniciar** y seleccione **todos los programas**.  
  
2.  Haga clic en el **SQL Server Migration Assistant para Access símbolo del sistema** acceso directo.  
  
    Muestra el menú de uso de la consola de SSMA y `(/? Help)`, que le ayudarán a empezar a trabajar con la aplicación de consola.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimiento para usar la consola SSMA  
Después de la consola se inicia correctamente en el sistema de Windows, podría utilizar los pasos siguientes para trabajar con ella:  
  
1.  Configurar la consola SSMA a través de los archivos de script. Para obtener más información acerca de esta sección, vea [crear archivos de Script &#40; AccessToSQL &#41; ](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Crear archivos de valor de la Variable &#40; AccessToSQL &#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Crear los archivos de conexión de servidor &#40; AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Ejecutar la consola SSMA &#40; AccessToSQL &#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) según sus necesidades de proyecto  
  
Características adicionales:  
  
1.  [Especifique una contraseña](http://msdn.microsoft.com/en-us/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) y exportar / importar en otros equipos de la ventana  
  
2.  [Generar informes](http://msdn.microsoft.com/en-us/abb4264a-622e-4215-af5b-14e309b8a399) ver el xml detallado informes de evaluación /conversion y migración de datos de salida. También se pueden generar informes de errores detallada para comandos de actualización y la sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de salida de consola SSMA  
Al ejecutar los comandos de script SSMA y opciones, el programa de consola muestra los resultados y mensajes (información, error, etc.) para el usuario en la consola o si es necesario, se redirige a un archivo de salida xml. Cada tipo de mensaje en la salida se especifica mediante un color único. Por ejemplo, el mensaje de texto en color blanco denota secuencias de comandos de archivo; uno de color verde representa un símbolo del sistema de entrada del usuario y así sucesivamente.  
  
![Salida de la consola SSMA](../../ssma/access/media/ssmaconsoleoutput.jpg "salida de la consola SSMA")  
  
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
[Instalar SQL Server Migration Assistant para Access](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)  
  
