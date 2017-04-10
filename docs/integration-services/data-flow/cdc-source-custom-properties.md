---
title: "Propiedades personalizadas del origen de CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Propiedades personalizadas del origen de CDC
  En la tabla siguiente se describen las propiedades personalizadas del origen de CDC. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|Conexión|Conexión ADO.Net|Conexión ADO.Net en la base de datos CDC de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para el acceso a las tablas de cambios.|  
|StateVariable|String|Variable de paquete de cadena SSIS que mantiene el estado CDC de la ejecución CDC actual.|  
|CdcProcessingMode|Integer (enumeración)|Este modo determina cómo se trata el procesamiento. Las opciones posibles son **Todo**, **Todo con valores antiguos**, **Neto**, **Neto con máscara de actualización**y **Neto con combinación**.<br /><br /> Los modos que comienzan por Todo devuelven todos los cambios y los modos que comienzan por Neto devuelven solo los cambios netos.<br /><br /> Las tablas sin una clave principal pueden tener solo valores TODO.<br /><br /> **Neto con máscara de actualización** agrega columnas booleanas con el patrón de nombre **__$\<nombre-columna>\__Changed** que indica las columnas cambiadas en la fila de cambio actual.<br /><br /> Para obtener información adicional sobre los valores de esta propiedad, vea [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).|  
|CaptureInstance|String|Nombre de la instancia de captura CDC con la tabla CDC que se va a leer. Una tabla de origen capturada puede tener una o dos instancias capturadas para controlar que la transición de una definición de tabla a través de los cambios en el esquema se realice sin problemas. Si se define más de una instancia de captura para la tabla de origen que se va a capturar, seleccione aquí la instancia de captura que desee usar. El nombre predeterminado de la instancia de captura para una tabla [esquema].[tabla] es \<esquema>_\<tabla>, pero los nombres de instancia de captura reales en uso podrían ser distintos. La tabla real de la que se lee es la tabla CDC **cdc .\<instancia-captura>_CT**.|  
|ReprocessingIndicator|Boolean|Valor que especifica si se debe agregar la columna **__$reprocessing**. Esta columna de salida especial permite al desarrollador de SSIS controlar los errores de coherencia de forma diferente cuando se trabaja en el intervalo de procesamiento inicial.<br /><br /> Si es **true**, se agrega la columna **__$reprocessing**.<br /><br /> El valor de esta columna es **true** cuando el intervalo de procesamiento CDC se solapa con el intervalo de procesamiento inicial (el intervalo de LSN que se corresponde al periodo de la carga inicial) o cuando un intervalo de procesamiento CDC se vuelve a procesar tras un error en una ejecución anterior. Con esta columna de indicador, el desarrollador de SSIS puede controlar los errores de manera diferente a cuando se vuelven a procesar los cambios (por ejemplo, se pueden omitir acciones como la eliminación de una fila que no existe o una inserción que causó un error en una clave duplicada).<br /><br /> El valor predeterminado es **false**.|  
|CommandTimeOut|Integer|Este valor indica el tiempo de espera (en segundos) para comunicarse con la base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se utiliza este valor siempre que el tiempo de respuesta de la base de datos sea muy breve y el valor predeterminado (30 segundos) no sea suficiente.|  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
  