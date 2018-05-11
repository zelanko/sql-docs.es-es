---
title: Columnas de datos de informes de progreso | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7d8dd07cbaf7ca4b9942b09f0f538a14a883e694
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="progress-reports-data-columns"></a>Columnas de datos de Informes de progreso
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La categoría de eventos Informes de progreso tiene las siguientes clases de eventos:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|Inicio del informe de progreso.|  
|6|Progress Report End|Final del informe de progreso.|  
|7|Progress Report Current|Informe de progreso en curso.|  
|8|Progress Report Error|Error del informe de progreso.|  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## <a name="progress-report-begindata-columns"></a>Columnas de datos de Progress Report Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Se definen los siguientes pares **Identificador de subclase**: **Nombre de subclase** válidos:<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Contiene el identificador de trabajo asociado al evento incluido en el informe.|  
|SessionType|8|8|Contiene el tipo de sesión (la entidad que produce el evento) asociada al evento incluido en el informe. Para procesar eventos, los valores son:<br /><br /> 1= Usuario<br /><br /> 2= Almacenamiento en caché automático<br /><br /> 3= Procesamiento diferido|  
|ObjectID|11|8|Contiene el identificador de objeto (una cadena) asociado al evento incluido en el informe.|  
|ObjectType|12|1|Contiene el tipo de objeto.|  
|ObjectName|13|8|Contiene el nombre del objeto asociado al evento incluido en el informe.|  
|ObjectPath|14|8|Contiene la ruta de acceso del objeto asociado al evento incluido en el informe, como una lista separada por comas de elementos primarios que empieza por los elementos primarios del objeto.|  
|ObjectReference|15|8|Contiene la referencia de objeto para el evento incluido en el informe, codificada como XML para todos los elementos primarios y con etiquetas para describir el objeto.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento incluido en el informe.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que ha tenido lugar el evento incluido en el informe.|  
|NTUserName|32|8|Contiene la cuenta de usuario de Windows asociada al evento incluido en el informe.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento incluido en el informe.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento incluido en el informe.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de manera única la sesión de usuario asociada al evento incluido en el informe. El SPID corresponde directamente al GUID de sesión usado por XML for Analysis (XMLA).|  
|TextData|42|9|Contiene los datos de texto asociados al evento incluido en el informe.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que ha tenido lugar el evento incluido en el informe.|  
  
## <a name="progress-report-enddata-columns"></a>Columnas de datos de Progress Report End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Se definen los siguientes pares **Identificador de subclase**: **Nombre de subclase** válidos:<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Contiene la cantidad de tiempo transcurrido (en milisegundos) que tarda el evento.|  
|CPUTime|6|2|Contiene la cantidad de tiempo de CPU (en milisegundos) usada por el evento.|  
|JobID|7|1|Contiene el identificador de trabajo asociado al evento incluido en el informe.|  
|SessionType|8|8|Contiene el tipo de sesión (la entidad que produce el evento) asociada al evento incluido en el informe. Para procesar eventos, los valores son:<br /><br /> 1= Usuario<br /><br /> 2= Almacenamiento en caché automático<br /><br /> 3= Procesamiento diferido|  
|ProgressTotal|9|1|Contiene el total del progreso para el evento incluido en el informe.|  
|IntegerData|10|1|Contiene los datos de enteros asociados al evento incluido en el informe, como el recuento actual del número de filas procesadas para un evento de procesamiento.|  
|ObjectID|11|8|Contiene el identificador de objeto (una cadena) asociado al evento incluido en el informe.|  
|ObjectType|12|1|Contiene el tipo de objeto.|  
|ObjectName|13|8|Contiene el nombre del objeto asociado al evento incluido en el informe.|  
|ObjectPath|14|8|Contiene la ruta de acceso del objeto asociado al evento incluido en el informe, como una lista separada por comas de elementos primarios que empieza por los elementos primarios del objeto.|  
|ObjectReference|15|8|Contiene la referencia de objeto para el evento incluido en el informe, codificada como XML para todos los elementos primarios y con etiquetas para describir el objeto.|  
|Severity|22|1|Contiene el nivel de gravedad de una excepción asociada al evento incluido en el informe. Los valores son:<br /><br /> 0 = Correcto.<br /><br /> 1 = De información<br /><br /> 2 = Advertencia<br /><br /> 3 = Error|  
|Success|23|1|Determina si el evento indicado por el servidor se realizó correctamente o no. Los valores son:<br /><br /> 0 = Error<br /><br /> 1 = Correcto|  
|Error|24|1|Contiene el número de error de un evento específico.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento incluido en el informe.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que ha tenido lugar el evento incluido en el informe.|  
|NTUserName|32|8|Contiene la cuenta de usuario de Windows asociada al evento incluido en el informe.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento incluido en el informe.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento incluido en el informe.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento incluido en el informe. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de manera única la sesión de usuario asociada al evento incluido en el informe. El SPID corresponde directamente al GUID de sesión usado por XML for Analysis (XMLA).|  
|TextData|42|9|Contiene los datos de texto asociados al evento incluido en el informe.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que ha tenido lugar el evento incluido en el informe.|  
  
## <a name="progress-report-currentdata-columns"></a>Columnas de datos de Progress Report Current  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Se definen los siguientes pares **Identificador de subclase**: **Nombre de subclase** válidos:<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Contiene el identificador de trabajo asociado al evento incluido en el informe.|  
|SessionType|8|8|Contiene el tipo de sesión (la entidad que produce el evento) asociada al evento incluido en el informe. Para procesar eventos, los valores son:<br /><br /> 1= Usuario<br /><br /> 2= Almacenamiento en caché automático<br /><br /> 3= Procesamiento diferido|  
|ProgressTotal|9|1|Contiene el total del progreso para el evento incluido en el informe.|  
|IntegerData|10|1|Contiene los datos de enteros asociados al evento incluido en el informe, como el recuento actual del número de filas procesadas para un evento de procesamiento.|  
|ObjectID|11|8|Contiene el identificador de objeto (una cadena) asociado al evento incluido en el informe.|  
|ObjectType|12|1|Contiene el tipo de objeto.|  
|ObjectName|13|8|Contiene el nombre del objeto asociado al evento incluido en el informe.|  
|ObjectPath|14|8|Contiene la ruta de acceso del objeto asociado al evento incluido en el informe, como una lista separada por comas de elementos primarios que empieza por los elementos primarios del objeto.|  
|ObjectReference|15|8|Contiene la referencia de objeto para el evento incluido en el informe, codificada como XML para todos los elementos primarios y con etiquetas para describir el objeto.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento incluido en el informe.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que ha tenido lugar el evento incluido en el informe.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento incluido en el informe.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de manera única la sesión de usuario asociada al evento incluido en el informe. El SPID corresponde directamente al GUID de sesión usado por XML for Analysis (XMLA).|  
|TextData|42|9|Contiene los datos de texto asociados al evento incluido en el informe.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que ha tenido lugar el evento incluido en el informe.|  
  
## <a name="progress-report-errordata-columns"></a>Columnas de datos de Progress Report Error  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Se definen los siguientes pares **Identificador de subclase**: **Nombre de subclase** válidos:<br /><br /> 1: **Process**<br /><br /> 2: **Merge**<br /><br /> 3: **Delete**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Rebuild**<br /><br /> 6: **Commit**<br /><br /> 7: **Rollback**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transaction**<br /><br /> 12: **Initialize**<br /><br /> 13: **Discretize**<br /><br /> 14: **Query**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Aggregate**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Connecting**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restore**<br /><br /> 39: **Synchronize**<br /><br /> 40: **Build Processing Schedule**<br /><br /> 41: **Detach**<br /><br /> 42: **Attach**<br /><br /> 43: **Analyze\Encode Data**<br /><br /> 44: **Compress Segment**<br /><br /> 45: **Write Table Column**<br /><br /> 46: **Relationship Build Prepare**<br /><br /> 47: **Build Relationship Segment**<br /><br /> 48: **Load**<br /><br /> 49: **Metadata Load**<br /><br /> 50: **Data Load**<br /><br /> 51: **Post Load**<br /><br /> 52: **Metadata traversal during Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Hierarchy processing**<br /><br /> 55: **Switching dictionary**|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Contiene la cantidad de tiempo transcurrido (en milisegundos) que tarda el evento.|  
|JobID|7|1|Contiene el identificador de trabajo asociado al evento incluido en el informe.|  
|SessionType|8|8|Contiene el tipo de sesión (la entidad que produce el evento) asociada al evento incluido en el informe. Para procesar eventos, los valores son:<br /><br /> 1= Usuario<br /><br /> 2= Almacenamiento en caché automático<br /><br /> 3= Procesamiento diferido|  
|ProgressTotal|9|1|Contiene el total del progreso para el evento incluido en el informe.|  
|IntegerData|10|1|Contiene los datos de enteros asociados al evento incluido en el informe, como el recuento actual del número de filas procesadas para un evento de procesamiento.|  
|ObjectID|11|8|Contiene el identificador de objeto (una cadena) asociado al evento incluido en el informe.|  
|ObjectType|12|1|Contiene el tipo de objeto.|  
|ObjectName|13|8|Contiene el nombre del objeto asociado al evento incluido en el informe.|  
|ObjectPath|14|8|Contiene la ruta de acceso del objeto asociado al evento incluido en el informe, como una lista separada por comas de elementos primarios que empieza por los elementos primarios del objeto.|  
|ObjectReference|15|8|Contiene la referencia de objeto para el evento incluido en el informe, codificada como XML para todos los elementos primarios y con etiquetas para describir el objeto.|  
|Severity|22|1|Contiene el nivel de gravedad de una excepción asociada al evento incluido en el informe. Los valores son:<br /><br /> 0 = Correcto.<br /><br /> 1 = De información<br /><br /> 2 = Advertencia<br /><br /> 3 = Error|  
|Error|24|1|Contiene el número de error de un evento específico.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento incluido en el informe.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que ha tenido lugar el evento incluido en el informe.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento incluido en el informe.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de manera única la sesión de usuario asociada al evento incluido en el informe. El SPID corresponde directamente al GUID de sesión usado por XML for Analysis (XMLA).|  
|TextData|42|9|Contiene los datos de texto asociados al evento incluido en el informe.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que ha tenido lugar el evento incluido en el informe.|  
  
## <a name="see-also"></a>Vea también  
 [Informes de progreso, categoría de eventos](../../analysis-services/trace-events/progress-reports-event-category.md)  
  
  
