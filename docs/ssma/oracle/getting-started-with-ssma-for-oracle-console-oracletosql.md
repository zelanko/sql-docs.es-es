---
title: "Introducción a SSMA para la consola de Oracle (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: "31"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f73c9250dd75d3beb5ec16cdb70fb3a4f7c57b20
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>Introducción a SSMA para la consola de Oracle (OracleToSQL)
Esta sección describe el procedimiento para iniciar y empezar a trabajar con la aplicación de consola de Oracle. También se muestran en este documento, se utilizan las convenciones en una ventana de salida de consola SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar la consola SSMA  
Utilice los pasos siguientes para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a **iniciar** y seleccione **todos los programas**.  
  
2.  Haga clic en el  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Oracle símbolo del sistema** acceso directo.  
  
    Muestra el menú de uso de la consola de SSMA y `(/? Help)`, que le ayudarán a empezar a trabajar con la aplicación de consola.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimiento para usar la consola SSMA  
Después de la consola se inicia correctamente en el sistema de Windows, podría utilizar los pasos siguientes para trabajar con ella:  
  
1.  Configurar la consola SSMA a través de los archivos de script. Para obtener más información acerca de esta sección, vea [crear archivos de Script &#40; OracleToSQL &#41;](../../ssma/oracle/creating-script-files-oracletosql.md) .  
  
2.  [Crear archivos de valor de la Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [Crear los archivos de conexión de servidor &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [Ejecutar la consola SSMA &#40; OracleToSQL &#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) según sus necesidades de proyecto  
  
Características adicionales:  
  
1.  [Especifique una contraseña](http://msdn.microsoft.com/en-us/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c) y exportar / importar en otros equipos de la ventana  
  
2.  [Generar informes](http://msdn.microsoft.com/en-us/ccad6262-01e1-447a-bd2b-c105154c80ce) ver el xml detallado informes de evaluación /conversion y migración de datos de salida. También se pueden generar informes de errores detallada para comandos de actualización y la sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de salida de consola SSMA  
Al ejecutar los comandos de script SSMA y opciones, el programa de consola muestra los resultados y mensajes (información, error, etc.) para el usuario en la consola o si es necesario, se redirige a un archivo de salida xml. Cada tipo de mensaje en la salida se especifica mediante un color único. Por ejemplo, el mensaje de texto en color blanco denota secuencias de comandos de archivo; uno de color verde representa un símbolo del sistema de entrada del usuario y así sucesivamente.  
  
![La consola ssma_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "consola ssma_oracle")  
  
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
[Instalación de SSMA para Oracle](http://msdn.microsoft.com/en-us/9211013a-ab24-4c52-9b26-87994b35e502)  
  
