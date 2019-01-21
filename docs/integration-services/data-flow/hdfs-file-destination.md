---
title: Destino de archivo HDFS | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f18f6b0516ab9ae417251e49f5a3cf24fd2aa997
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185011"
---
# <a name="hdfs-file-destination"></a>HDFS File Destination
  El componente HDFS File Destination (Destino de archivo HDFS) permite que un paquete SSIS escriba datos en un archivo HDFS. Los formatos de archivo admitidos son Text, Avro y ORC.  
  
 Para configurar el componente HDFS File Destination, arrastre y coloque el componente HDFS File Source (Origen de archivo HDFS) en el diseñador de flujo de datos y haga doble clic en el componente para abrir el editor.  
  
 ![Editor de destino de archivo HDFS](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS File Destination Editor")  
  
## <a name="options"></a>Opciones  
 Configure las siguientes opciones en la pestaña **General** del cuadro de diálogo **Hadoop File Destination Editor** (Editor de destino de archivo Hadoop).  
  
|Campo|Descripción|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos HDFS.|  
|**Ruta del archivo**|Especifique el nombre del archivo HDFS.|  
|**Formato de archivo**|Especifique el formato del archivo HDFS. Las opciones disponibles son Text, Avro y ORC.|  
|**Carácter delimitador de columna**|Si selecciona el formato Text, especifique el carácter delimitador de columna.|  
|**Nombres de columna de la primera fila de datos**|Si selecciona el formato Text, indique si la primera fila del archivo contiene nombres de columnas.|  
  
 Después de configurar estas opciones, seleccione la pestaña **Columna** para asignar columnas de origen a columnas de destino del flujo de datos.  

::: moniker range=">= sql-server-ver15"
## <a name="prerequisite-for-orc-format"></a>Requisito previo para el formato ORC

Para poder usar el formato de archivo ORC, tendrá que instalar Java Runtime Environment (JRE) versión 1.7.51 o posterior para la plataforma adecuada.

Se admiten los JRE de Zulu y Oracle.
-   [JRE de Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
-   [JRE de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

### <a name="set-up-the-zulu-jre"></a>Configuración del JRE de Zulu

1. Descargue y extraiga el paquete ZIP de instalación OpenJDK de Zulu.

2.  Desde el símbolo del sistema, ejecute `sysdm.cpl`.

3. En la pestaña **Avanzadas**, haga clic en **Variables de entorno**.

4. En la sección **Variables del sistema**, haga clic en **Nueva**.

5. Escriba `JAVA_HOME` para el **Nombre de variable**.

6. Haga clic en **Examinar directorio**, navegue hasta la carpeta de instalación de OpenJDK de Zulu y haga clic en la subcarpeta `jre`. Después, haga clic en Aceptar. El valor de la variable se rellena de forma automática.

7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Nueva variable del sistema**.

8. Haga clic en **Aceptar** para cerrar el cuadro de diálogo Variables de entorno.

### <a name="set-up-the-oracle-jre"></a>Configuración del JRE de Oracle

1. Descargue y ejecute el programa de instalación .exe del JRE de Oracle.

1. Siga las instrucciones del programa de instalación para completar la instalación.

::: moniker-end

## <a name="see-also"></a>Consulte también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Origen de archivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)  
