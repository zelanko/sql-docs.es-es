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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6a18a12c10e23e44b597ec6dc5bddebf6a5a77db
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275788"
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

## <a name="prerequisite-for-orc-file-format"></a>Requisito previo para el formato de archivo ORC
Para usar el formato de archivo ORC se necesita Java.
La arquitectura (32 o 64 bits) de la compilación de Java debe coincidir con la del runtime de SSIS que se va a usar.
Se han probado las siguientes compilaciones de Java.

- [OpenJDK 8u192 de Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Java SE Runtime Environment 8u192 de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurar OpenJDK de Zulu
1. Descargue y extraiga el paquete ZIP de instalación.
2. Desde el símbolo del sistema, ejecute `sysdm.cpl`.
3. En la pestaña **Avanzadas**, haga clic en **Variables de entorno**.
4. En la sección **Variables del sistema**, haga clic en **Nueva**.
5. Escriba `JAVA_HOME` para el **Nombre de variable**.
6. Seleccione **Examinar directorio**, vaya a la carpeta extraída y seleccione la subcarpeta `jre`.
   Luego seleccione **Aceptar** y el campo **Valor de la variable** se rellena de forma automática.
7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Nueva variable del sistema**.
8. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Variables de entorno**.
9. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades del sistema**.

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurar Java SE Runtime Environment de Oracle
1. Descargue y ejecute el instalador .exe.
2. Siga las instrucciones del programa de instalación para completar la instalación.

::: moniker-end

## <a name="see-also"></a>Consulte también
[Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
[Origen de archivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)
