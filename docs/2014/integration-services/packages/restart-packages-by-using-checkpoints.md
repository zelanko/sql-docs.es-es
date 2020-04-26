---
title: Reiniciar paquetes usando puntos de comprobación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f41ed858bedd18ec68794d5e7d1c13100af5254
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767037"
---
# <a name="restart-packages-by-using-checkpoints"></a>Reiniciar paquetes de usando puntos de comprobación
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede reiniciar los paquetes con errores desde el punto del error, en lugar de volver a ejecutar todo el paquete. Si se configura un paquete para que utilice puntos de comprobación, la información relacionada con la ejecución del paquete se escribirá en un archivo de punto de comprobación. Cuando se vuelve a ejecutar el paquete con error, se utiliza el archivo de punto de comprobación para reiniciar el paquete desde el punto del error. Si el paquete se ejecuta correctamente, el archivo de punto de comprobación se elimina y se vuelve a crear la siguiente vez que se ejecuta el paquete.  
  
 El uso de puntos de comprobación en un paquete puede proporcionar las siguientes ventajas.  
  
-   Evita que se repita la descarga y la carga de archivos grandes. Por ejemplo, un paquete que descarga varios archivos grandes mediante una tarea de FTP para cada descarga, se puede reiniciar cuando la descarga de un solo archivo genera un error y, a continuación, descargar únicamente ese archivo.  
  
-   Evita repetir la carga de grandes cantidades de datos. Por ejemplo, un paquete que realiza inserciones masivas en tablas de dimensiones de un almacenamiento de datos, utilizando una tarea Inserción masiva para cada dimensión, se puede reiniciar si la inserción genera un error para una tabla de dimensión y, en ese caso, solo se volverá a cargar esa dimensión.  
  
-   Evita repetir la agregación de valores. Por ejemplo, un paquete que calcula muchos agregados, como promedios y sumas, utilizando una tarea Flujo de datos para realizar cada agregación, se puede reiniciar cuando el cálculo de una agregación genera un error, y solo se vuelve a calcular esa agregación.  
  
 Si un paquete está configurado para utilizar puntos de comprobación, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] captura el punto de reinicio del archivo de punto de comprobación. El tipo de contenedor que genera el error y la implementación de características como las transacciones afectan al punto de reinicio que se registra en el archivo de punto de comprobación. Los valores actuales de variables se capturan también en el archivo de punto de comprobación. Sin embargo, los valores de variables que tienen el tipo de datos `Object` no se guardan en los archivos de punto de comprobación.  
  
## <a name="defining-restart-points"></a>Definir puntos de reinicio  
 El contenedor host de la tarea, que encapsula una sola tarea, es la unidad atómica de trabajo más pequeña que se puede reiniciar. El contenedor de bucles Foreach y un contenedor de transacción también se tratan como unidades atómicas de trabajo.  
  
 Si se detiene un paquete mientras se está ejecutando un contenedor de transacción, la transacción finaliza y se revierte todo el trabajo realizado por el contenedor. Cuando se reinicia el paquete, se vuelve a ejecutar el contenedor que generó el error. La finalización de los contenedores secundarios del contenedor de transacción no se registra en el archivo de punto de comprobación. Por lo tanto, cuando se reinicia el paquete, se vuelve a ejecutar el contenedor de transacción con todos sus contenedores secundarios.  
  
> [!NOTE]  
>  Utilizar puntos de comprobación y transacciones en el mismo paquete podría producir resultados inesperados. Por ejemplo, cuando un paquete genera un error y se reinicia desde un punto de comprobación, podría repetir una transacción que ya se ha confirmado correctamente.  
  
 Los datos de punto de comprobación no se guardan para los contenedores de bucles For y Foreach. Cuando se reinicia un paquete, se vuelven a ejecutar el contenedor de bucles For y Foreach y sus contenedores secundarios. Si un contenedor secundario en el bucle se ejecuta correctamente, no se graba en el archivo de punto de comprobación sino que se vuelve a ejecutar. Para obtener más información y solucionar este problema, vea [Los puntos de comprobación de SSIS no se respetan para los elementos de contenedor de bucles For y Foreach](https://go.microsoft.com/fwlink/?LinkId=241633).  
  
 Si se reinicia el paquete, las configuraciones de paquetes no se vuelven a cargar sino que se utiliza la información de configuración escrita en el archivo de punto de comprobación. Esto asegura que, el paquete utilice las mismas configuraciones cuando se vuelva a ejecutar que cuando sufrió el error.  
  
 Un paquete solamente se puede reiniciar en el nivel de flujo de control. No puede reiniciar un paquete a mitad de un flujo de datos. Para evitar volver a ejecutar el flujo de datos entero, el paquete podría estar diseñado para incluir varios flujos de datos, cada uno utilizando una tarea Flujo de datos diferente. Esta manera que se puede reiniciar el paquete, volviendo a ejecutar solo una tarea Flujo de datos.  
  
## <a name="configuring-a-package-to-restart"></a>Configurar un paquete para que se reinicie  
 El archivo de punto de comprobación incluye los resultados de ejecución de todos los contenedores completados, los valores actuales de las variables del sistema y las definidas por el usuario, y la información de configuración de paquetes. El archivo también incluye el identificador único del paquete. Para reiniciar correctamente un paquete, el identificador del paquete en el archivo de punto de comprobación y el paquete deben coincidir; de lo contrario, no se podrá reiniciar. Esto evita que un paquete utilice un archivo de punto de comprobación escrito por una versión distinta del paquete. Si el paquete se ejecuta correctamente, el archivo de punto de comprobación se elimina después de reiniciar el paquete.  
  
 En la tabla siguiente se muestran las propiedades del paquete establecidas para implementar puntos de comprobación.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|CheckpointFileName|Especifica el nombre del archivo de punto de comprobación.|  
|CheckpointUsage|Especifica si se utilizarán puntos de comprobación.|  
|SaveCheckpoints|Indica si el paquete guarda puntos de comprobación. Esta propiedad debe estar establecida en True para poder reiniciar un paquete desde el punto del error.|  
  
 Además, debe establecer la propiedad FailPackageOnFailure en `true` para todos los contenedores del paquete que desea identificar como puntos de reinicio.  
  
 Puede usar la propiedad ForceExecutionResult para probar el uso de los puntos de comprobación de un paquete. Si establece ForceExecutionResult de una tarea o un contenedor en Error, puede simular un error en tiempo real. Al volver a ejecutar el paquete, se volverá a ejecutar la tarea que generó el error y los contenedores.  
  
### <a name="checkpoint-usage"></a>Usar puntos de comprobación  
 La propiedad CheckpointUsage se puede establecer en los siguientes valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|`Never`|Especifica que no se utilizará el archivo de punto de comprobación y que el paquete se ejecutará desde el inicio del flujo de trabajo del paquete.|  
|`Always`|Especifica que el archivo de punto de comprobación se utilizará siempre y que el paquete se reinicia desde el punto del error de ejecución anterior. Si no se encuentra el archivo de punto de comprobación, el paquete generará un error.|  
|`IfExists`|Especifica que se utilizará el archivo de punto de comprobación, si existe. Si existe un archivo de punto de comprobación, el paquete se reiniciará desde el punto del error de ejecución anterior; de lo contrario, se ejecutará desde el inicio del flujo de trabajo del paquete.|  
  
> [!NOTE]  
>  La opción **/Checkpointing on on** de DTExec es equivalente a establecer la `SaveCheckpoints` propiedad del paquete en `True`y la `CheckpointUsage` propiedad en Always. Para obtener más información, consulte [utilidad dtexec](dtexec-utility.md).  
  
## <a name="securing-checkpoint-files"></a>Proteger archivos de puntos de comprobación  
 El nivel de protección de paquetes no incluye la protección de archivos de puntos de comprobación; estos archivos se deben proteger por separado. Solo puede almacenar datos de puntos de comprobación en el sistema de archivos y debe utilizar una lista de control de acceso (ACL) al sistema operativo para proteger la ubicación o carpeta en la que ha almacenado el archivo. Es importante proteger los archivos de puntos de comprobación, dado que contienen información sobre el estado del paquete, incluidos los valores actuales de las variables. Por ejemplo, una variable puede contener un conjunto de registros con varias filas de datos privados, tales como números de teléfono. Para más información, vea [Acceso a los archivos usados por los paquetes](../access-to-files-used-by-packages.md).  
  
### <a name="to-configure-the-checkpoint-properties"></a>Para configurar las propiedades del punto de comprobación  
  
-   [Configurar puntos de comprobación para reiniciar un paquete con error](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>Recursos externos  
  
-   El artículo técnico sobre el [reinicio automático de paquetes SSIS tras una conmutación por error o un error](https://go.microsoft.com/fwlink/?LinkId=200407), en social.technet.microsoft.com.  
  
-   El artículo de soporte técnico, [Los puntos de comprobación de SSIS no se respetan para los elementos de contenedor de bucles For y Foreach](https://go.microsoft.com/fwlink/?LinkId=241633), en support.microsoft.com.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
