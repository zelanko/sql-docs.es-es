---
title: Columnas de datos de informes de progreso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Progress Reports event category
ms.assetid: d34a6322-e26b-4454-b98f-32307d6956b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8569f18f3838116ea5a1ed045f418602f85032c6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171175"
---
# <a name="progress-reports-data-columns"></a>Columnas de datos de Informes de progreso
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
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: proceso<br /><br /> 2: fusionar mediante combinación<br /><br /> 3: eliminar<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: volver a generar<br /><br /> 6: confirmar<br /><br /> 7: reversión<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transacciones<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregado<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: segmentos<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: copia de seguridad<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: programación de procesamiento de compilación<br /><br /> 41: desasociar<br /><br /> 42: conectar<br /><br /> 43: Analyze\Encode datos<br /><br /> 44: comprimir segmento<br /><br /> 45: escribir la columna de tabla<br /><br /> 46: preparar la compilación de relación<br /><br /> 47: crear segmento de relación<br /><br /> 48: carga<br /><br /> 49: carga de metadatos<br /><br /> 50: carga de datos<br /><br /> 51: postcarga<br /><br /> 52: del recorrido de metadatos durante la copia de seguridad<br /><br /> 53: VertiPaq<br /><br /> 54: procesamiento de jerarquía<br /><br /> 55: cambio de diccionario|  
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
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: proceso<br /><br /> 2: fusionar mediante combinación<br /><br /> 3: eliminar<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: volver a generar<br /><br /> 6: confirmar<br /><br /> 7: reversión<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transacciones<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregado<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: segmentos<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: copia de seguridad<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: programación de procesamiento de compilación<br /><br /> 41: desasociar<br /><br /> 42: conectar<br /><br /> 43: Analyze\Encode datos<br /><br /> 44: comprimir segmento<br /><br /> 45: escribir la columna de tabla<br /><br /> 46: preparar la compilación de relación<br /><br /> 47: crear segmento de relación<br /><br /> 48: carga<br /><br /> 49: carga de metadatos<br /><br /> 50: carga de datos<br /><br /> 51: postcarga<br /><br /> 52: del recorrido de metadatos durante la copia de seguridad<br /><br /> 53: VertiPaq<br /><br /> 54: procesamiento de jerarquía<br /><br /> 55: cambio de diccionario|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Contiene la cantidad de tiempo transcurrido (en milisegundos) que tarda el evento.|  
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
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: proceso<br /><br /> 2: fusionar mediante combinación<br /><br /> 3: eliminar<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: volver a generar<br /><br /> 6: confirmar<br /><br /> 7: reversión<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transacciones<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregado<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: segmentos<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: copia de seguridad<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: programación de procesamiento de compilación<br /><br /> 41: desasociar<br /><br /> 42: conectar<br /><br /> 43: Analyze\Encode datos<br /><br /> 44: comprimir segmento<br /><br /> 45: escribir la columna de tabla<br /><br /> 46: preparar la compilación de relación<br /><br /> 47: crear segmento de relación<br /><br /> 48: carga<br /><br /> 49: carga de metadatos<br /><br /> 50: carga de datos<br /><br /> 51: postcarga<br /><br /> 52: del recorrido de metadatos durante la copia de seguridad<br /><br /> 53: VertiPaq<br /><br /> 54: procesamiento de jerarquía<br /><br /> 55: cambio de diccionario|  
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
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: proceso<br /><br /> 2: fusionar mediante combinación<br /><br /> 3: eliminar<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: volver a generar<br /><br /> 6: confirmar<br /><br /> 7: reversión<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transacciones<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregado<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: segmentos<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: copia de seguridad<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: programación de procesamiento de compilación<br /><br /> 41: desasociar<br /><br /> 42: conectar<br /><br /> 43: Analyze\Encode datos<br /><br /> 44: comprimir segmento<br /><br /> 45: escribir la columna de tabla<br /><br /> 46: preparar la compilación de relación<br /><br /> 47: crear segmento de relación<br /><br /> 48: carga<br /><br /> 49: carga de metadatos<br /><br /> 50: carga de datos<br /><br /> 51: postcarga<br /><br /> 52: del recorrido de metadatos durante la copia de seguridad<br /><br /> 53: VertiPaq<br /><br /> 54: procesamiento de jerarquía<br /><br /> 55: cambio de diccionario|  
|CurrentTime|2|5|Contiene la hora actual del evento incluido en el informe, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Contiene la cantidad de tiempo transcurrido (en milisegundos) que tarda el evento.|  
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
 [Categoría de eventos Informes de progreso](progress-reports-event-category.md)  
  
  
