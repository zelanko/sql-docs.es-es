---
title: Introducción con SSMA para la consola de DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fbb0a90d9cfd628e9251a55de3df8b66a22f1ef7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67989659"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Introducción con SSMA para la consola de DB2 (DB2ToSQL)
En esta sección se describe el procedimiento para iniciar y comenzar a usar la aplicación de consola DB2. Además, aquí se enumeran las convenciones que se usan en una ventana de salida de la consola de SSMA típica.  
  
## <a name="launching-ssma-console"></a>Inicio de la consola SSMA  
Siga estos pasos para iniciar la aplicación de consola SSMA:  
  
1.  Vaya a **Inicio** y seleccione **todos los programas**.  
  
2.  Haga clic en el acceso directo del ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] símbolo del sistema de Migration Assistant para DB2** .  
  
    Muestra el menú de uso de la consola `(/? Help)`de SSMA y, para ayudarle a empezar a trabajar con la aplicación de consola.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimiento para usar la consola de SSMA  
Una vez que se haya iniciado correctamente la consola de en el sistema Windows, puede usar los pasos siguientes para trabajar en ella:  
  
1.  Configure la consola de SSMA a través de los archivos de script. Para obtener más información sobre esta sección, vea [crear archivos de Script &#40;DB2ToSQL&#41;](../../ssma/db2/creating-script-files-db2tosql.md) .  
  
2.  [Crear archivos de valores de variable &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [Crear los archivos de conexión del servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [Ejecutar la consola de SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md) según las necesidades del proyecto  
  
Características adicionales:  
  
1.  [Administración de contraseñas](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) y exportación e importación en otras máquinas Windows  
  
2.  [Generación de informes](https://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883) para ver los informes de salida XML detallados para la evaluación de/conversion y la migración de datos. También se pueden generar informes de errores detallados para los comandos de actualización y sincronización.  
  
## <a name="ssma-console-output-conventions"></a>Convenciones de salida de la consola SSMA  
Al ejecutar los comandos y las opciones de script de SSMA, el programa de consola muestra los resultados y los mensajes (información, error, etc.) al usuario en la consola de o, si es necesario, redirige a un archivo de salida XML. Cada tipo de mensaje de la salida se indica mediante un color único. Por ejemplo, el mensaje de texto en color blanco denota los comandos del archivo de script; el color verde representa un mensaje para la entrada del usuario, etc.  
  
![Salida de la consola SSMA_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "Salida de la consola SSMA_Oracle")  
  
Interpretación de color de la salida de la consola en la tabla siguiente:  
  
|Color|Descripción|  
|---------|---------------|  
|Rojo|Error irrecuperable durante la ejecución|  
|Gris|Marca de fecha y hora, mensaje al usuario|  
|Blanco|Comandos de archivo de script, tipo de mensaje|  
|Amarillo|Advertencia|  
|Verde|Solicitar la entrada del usuario|  
|Cian|Inicio, finalización y resultado de una operación|  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para DB2](https://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
