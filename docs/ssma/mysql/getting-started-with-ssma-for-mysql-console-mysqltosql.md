---
description: Introducción a SSMA para la consola de MySQL (MySQLToSQL)
title: Introducción con SSMA para la consola de MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9eba640bc529487772510e06a7c66210be3e43a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463444"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Introducción a SSMA para la consola de MySQL (MySQLToSQL)
En esta sección se describe el procedimiento para iniciar y comenzar a usar la aplicación de consola de MySQL. Además, aquí se enumeran las convenciones que se usan en una ventana de salida de la consola de SSMA típica.  
  
## <a name="launching-ssma-console"></a>Inicio de la consola SSMA  
Siga estos pasos para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a **Inicio** y seleccione **todos los programas**.  
  
2.  Haga clic en el acceso directo del **símbolo del sistema de SQL Server Migration Assistant para MySQL** .  
  
    Muestra el menú de uso de la consola de SSMA y `(/? Help)` , para ayudarle a empezar a trabajar con la aplicación de consola.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimiento para usar la consola de SSMA  
Una vez que se haya iniciado correctamente la consola de en el sistema Windows, puede usar los pasos siguientes para trabajar en ella:  
  
1.  Configure la consola de SSMA a través de los archivos de script. Para obtener más información sobre esta sección, vea [crear archivos de Script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md) .  
  
2.  [Crear archivos de valores de variable &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [Crear los archivos de conexión del servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [Ejecutar la consola de SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) según las necesidades del proyecto  
  
Características adicionales:  
  
1.  [Protección](managing-passwords-mysqltosql.md) de la contraseña y exportación e importación en otras máquinas de Windows  
  
2.  [Generar informes](generating-reports-mysqltosql.md) para ver los informes de salida XML detallados para la evaluación de/conversion y la migración de datos. También se pueden generar informes de errores detallados para los comandos de actualización y sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de salida de la consola SSMA  
Al ejecutar los comandos y las opciones de script de SSMA, el programa de consola muestra los resultados y los mensajes (información, error, etc.) al usuario en la consola de o, si es necesario, redirige a un archivo de salida XML. Cada tipo de mensaje de la salida se indica mediante un color único. Por ejemplo, el mensaje de texto en color blanco denota los comandos del archivo de script; el color verde representa un mensaje para la entrada del usuario, etc.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
Interpretación de color de la salida de la consola en la tabla siguiente:  
  
|Color|Descripción|  
|---------|---------------|  
|Rojo|Error irrecuperable durante la ejecución|  
|Gris|Marca de fecha y hora, mensaje al usuario|  
|Blanco|Comandos de archivo de script, tipo de mensaje|  
|Amarillo|Advertencia|  
|Verde|Solicitar la entrada del usuario|  
|Cian|Inicio, finalización y resultado de una operación|  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para MySQL](installing-ssma-for-mysql-mysqltosql.md)  
  
