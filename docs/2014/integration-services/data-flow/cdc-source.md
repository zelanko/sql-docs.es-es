---
title: Origen CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 80e557d9d286040b1d145c852779a9eca5cd4e64
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382731"
---
# <a name="cdc-source"></a>origen de CDC
  El origen CDC lee un intervalo de datos modificados de las tablas de cambios de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y entrega los cambios de nivel inferior a otros componentes de SSIS.  
  
 El intervalo de lectura de los datos modificados por el origen CDC se denomina intervalo de procesamiento CDC y se determina con la tarea Control CDC que se ejecuta antes de que el flujo de datos actual se inicie. El intervalo de procesamiento CDC se deriva del valor de una variable de paquete que mantiene el estado del procesamiento CDC para un grupo de tablas.  
  
 El origen CDC extrae los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una tabla de base de datos, una vista o una instrucción SQL.  
  
 El origen CDC utiliza las configuraciones siguientes:  
  
-   Administrador de conexiones ADO.NET de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información sobre cómo configurar la conexión de origen CDC, vea [CDC Source Editor &#40;Connection Manager Page&#41;](../cdc-source-editor-connection-manager-page.md).  
  
-   Tabla habilitada para CDC.  
  
-   Nombre de la instancia de captura de la tabla seleccionada (si existe más de una).  
  
-   Modo del procesamiento de cambios.  
  
-   Nombre de la variable de paquete de estado CDC basado en lo que determina el intervalo de procesamiento CDC. El origen CDC no modifica esa variable.  
  
 Los datos devueltos por el origen CDC son los mismos que los devueltos por las funciones CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** o **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** (si estuvieran disponibles). La única adición opcional es la columna **__$initial_processing** , que indica si el intervalo de procesamiento actual puede solaparse con una carga inicial de la tabla. Para obtener más información acerca del procesamiento inicial, vea [CDC Control Task](../control-flow/cdc-control-task.md).  
  
 El origen de CDC tiene una salida normal y una salida de error.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El origen de CDC tiene una salida de error. La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: El valor es siempre -1.  
  
-   **Columna de error**: La columna de origen que produce el error (para errores de conversión).  
  
-   **Columnas de la fila de error**: Los datos del registro que ocasionan el error.  
  
 Según la configuración del comportamiento de los errores, el origen CDC permite devolver los errores (conversión de datos, truncamiento) que aparecerán durante el proceso de extracción en la salida de error. Para más información, vea [CDC Source Editor &#40;Error Output Page&#41;](../cdc-source-editor-error-output-page.md).  
  
## <a name="data-type-support"></a>Compatibilidad con tipos de datos  
 El componente de origen CDC para Microsoft admite todos los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que se asignan a los tipos de datos de SSIS correctos.  
  
## <a name="troubleshooting-the-cdc-source"></a>Solucionar problemas del origen de CDC  
 A continuación se muestra información para solucionar problemas del origen de CDC.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>Use este script para aislar los problemas y reproducirlos en SQL Server Management Studio  
 La operación de origen de CDC se rige por la operación de la tarea Control CDC ejecutada antes de invocar al origen de CDC. La tarea Control CDC prepara el valor de la variable de paquete de estado CDC para contener los LSN inicial y final. Realiza la función equivalente a la del script siguiente:  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 donde:  
  
-   \<cdc-enabled-database-name> es del nombre de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene las tablas de cambios.  
  
-   \<value-from-state-cs> es el valor que aparece en la variable de estado CDC como CS/\<value-from-state-cs>/ (CS representa el inicio del intervalo de procesamiento actual [Current-processing-range-Start]).  
  
-   \<value-from-state-ce> es el valor que aparece en la variable de estado CDC como CE/\<value-from-state-cs>/ (CE representa el final del intervalo de procesamiento actual [Current-processing-range-End]).  
  
-   \<mode> son los modos de procesamiento de CDC. Los modos de procesamiento tienen uno de los siguientes valores **Todo**, **Todo con valores antiguos**, **Neto**, **Neto con máscara de actualización**, **Neto con combinación**.  
  
 Este script ayuda a aislar los problemas reproduciéndolos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], donde resulta sencillo reproducir e identificar los errores.  
  
#### <a name="sql-server-error-message"></a>Mensaje de error de SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]podría devolver el mensaje siguiente:  
  
 **Se ha especificado un número insuficiente de argumentos para el procedimiento o función cdc.fn_cdc_get_net_changes_ \<..>.**  
  
 Este error indica que falta un argumento. Indica que los valores de LSN inicial o final de la variable de estado CDC no son válidos.  
  
## <a name="configuring-the-cdc-source"></a>Configurar el origen de CDC  
 Puede configurar el origen de CDC mediante programación o través del Diseñador SSIS.  
  
 Para obtener más información, vea uno de los siguientes temas:  
  
-   [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de CDC &#40;página Columnas&#41;](../cdc-source-editor-columns-page.md)  
  
-   [Editor de origen de CDC &#40;página Salida de error&#41;](../cdc-source-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el origen CDC y seleccione **Mostrar editor avanzado**.  
  
 Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo **Editor avanzado** , vea [CDC Source Custom Properties](cdc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de CDC &#40;página Columnas&#41;](../cdc-source-editor-columns-page.md)  
  
-   [Editor de origen de CDC &#40;página Salida de error&#41;](../cdc-source-editor-error-output-page.md)  
  
-   [CDC Source Custom Properties](cdc-source-custom-properties.md)  
  
-   [Extraer datos de modificaciones mediante el origen de CDC](cdc-source.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada del blog, sobre [Modos de procesamiento para el origen CDC](https://go.microsoft.com/fwlink/?LinkId=242541), en mattmasson.com.  
  
  
