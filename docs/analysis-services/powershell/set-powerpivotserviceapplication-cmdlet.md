---
title: Cmdlet Set-PowerPivotServiceApplication | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 16d10e2d-d7e1-40f1-bc9d-a4e10c61af95
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0def855b93ce209aa923fd57e60d01c142a7fd0d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Cmdlet Set-PowerPivotServiceApplication
  
 [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)] 

  Establece las propiedades de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet Set-PowerPivotServiceApplication actualiza las propiedades de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. El parámetro Identity es obligatorio. Debe proporcionar el GUID de la aplicación de servicio para la que desea actualizar las propiedades.  
  
 Para comprobar los cambios, ejecute el siguiente cmdlet: Get-PowerPivotServiceApplication-Identity \<GUID > | lista formato.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Especifica la aplicación de servicio que se va a actualizar. El tipo debe ser un GUID válido o una instancia de un objeto válido de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Puede usar Get-PowerPivotServiceApplication para devolver una instancia de objeto.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<int >  
 Especifica el número de conexiones abiertas en un grupo de conexiones creado para una conexión de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a Analysis Services. Cada instancia de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] abre una conexión administrativa independiente a la instancia de Analysis Services en el mismo equipo. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] crea un grupo independiente para reutilizar las conexiones administrativas con el propósito de comprobar si hay conexiones inactivas y supervisar el estado del servidor. El valor predeterminado es de 200 conexiones. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de administrador), o de 1 a 10.000. Si selecciona 0, cada conexión se creará como nueva.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|200|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<SwitchParameter >]  
 Especifica si los propietarios de programaciones pueden escribir credenciales de Windows arbitrarias para ejecutar una programación de actualización de datos. Si activa esta casilla, la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creará y administrará una aplicación de destino para cada conjunto de credenciales almacenadas. De manera predeterminada, se establece en true. Para desactivar esta característica, establezca AllowCustomWindowsCredentials:$false.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime \<cadena >  
 Especifica el extremo de un intervalo de horas que definen un día laboral. Las programaciones de actualización de datos pueden ejecutarse al terminar un día laborable a fin de reunir los datos de las transacciones que se generaron durante las horas de trabajo normales. El valor predeterminado es 8:00 p.m.  Los valores válidos se especifican entre comillas, en a.m. o p.m. hora de reloj (por ejemplo, "08:00p.m". Las horas deben ser un valor comprendido entre 1 y 12. Los minutos deben ser un valor comprendido entre 1 y 59.  
  
 Para especificar el intervalo completo de horas de un día laborable, debe establecer BusinessHoursStartTime y BusinessHoursEndTime. Los dos parámetros definen el intervalo de horas que componen un día laborable.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|8 p.m.|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime \<cadena >  
 Especifica el punto de inicio de un intervalo de horas que definen un día laboral. Las programaciones de actualización de datos pueden ejecutarse al terminar un día laborable a fin de reunir los datos de las transacciones que se generaron durante las horas de trabajo normales. El valor predeterminado es las 4:00 a.m.  Los valores válidos se especifican entre comillas, en a.m. o p.m. hora de reloj (por ejemplo, "04:00a.m". Las horas deben ser un valor comprendido entre 1 y 12. Los minutos deben ser un valor comprendido entre 1 y 59.  
  
 Para especificar el intervalo completo de horas de un día laborable, debe establecer BusinessHoursStartTime y BusinessHoursEndTime. Los dos parámetros definen el intervalo de horas que componen un día laborable.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|4 a.m.|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<int >  
 Especifica cuántas horas permanece inactiva una base de datos en el sistema de archivos una vez descargada de la memoria. El valor predeterminado es 120 horas. El trabajo de limpieza usa este valor para determinar qué archivos eliminar. El trabajo de limpieza elimina del disco todas las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que hayan estado inactivas 168 horas (48 horas en memoria y 120 horas en memoria caché).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|120|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-confirm-switch"></a>-Confirme \<cambiar >  
 Le solicita confirmación antes de ejecutar el comando. Este valor se habilita de forma predeterminada. Para omitir la respuesta de confirmación de un comando, especifique Confirm:$false en el comando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-connectionpoolsize-int"></a>-ConnectionPoolSize \<int >  
 Especifica el número máximo de conexiones inactivas que el servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creará en grupos de conexiones individuales para cada usuario de SharePoint, conjunto de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y combinaciones de versión. El valor predeterminado es de 1000 conexiones inactivas. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de usuario), o de 1 a 10000. Estos grupos de conexiones permiten al servicio admitir más eficazmente conexiones continuadas a los mismos datos de solo lectura del mismo usuario. Si deshabilita la agrupación de conexiones, cada conexión se creará como nueva. Observe que cambiar el límite del tamaño del grupo de conexiones, incluso si se establece en 0, no hará que se quiten conexiones. Los grupos de conexiones existen para reducir los tiempos de espera al conectar a los datos. El servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nunca denegará una conexión según la configuración del grupo de conexiones.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|1000|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<int >  
 Especifica cuántos minutos permanecerá abierta una conexión de datos inactiva. El valor predeterminado es 1800 segundos (o 30 minutos). Durante este período, la aplicación del servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] reutilizará una conexión de datos inactiva para las solicitudes de solo lectura del mismo usuario de SharePoint para los mismos datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si no se reciben más solicitudes para esos datos durante el período especificado, la conexión se quita del conjunto. Los valores válidos van de 1 a 3600 segundos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|1800|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<int >  
 Especifica cuánto tiempo espera la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] una respuesta de la instancia de SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) a la que se ha reenviado una solicitud de carga de datos. Dado que los conjuntos de datos muy grandes tardan tiempo en atravesar la conexión, debe permitir el tiempo suficiente para que la instancia de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recupere el libro de Excel y mueva los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una instancia de Analysis Services para que se procesen las consultas. El valor predeterminado es 1800 segundos (o 30 minutos). Los valores válidos oscilan entre 1 y 3600 segundos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|1800|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<int >  
 Especifica el número de errores consecutivos después del cual una programación se deshabilita. El valor predeterminado es 10. También puede escribir 0 para no deshabilitar nunca una programación debido a errores de la actualización.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|10|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<int >  
 Especifique el número de ciclos de actualización de datos tras los que una programación se deshabilita o escriba 0 para no deshabilitar nunca una programación debido a la inactividad. El valor predeterminado es 10 ciclos.  
  
 La inactividad del libro se mide como la ausencia de eventos de conexión en varios ciclos de actualización de datos. Un ciclo de actualización de datos se cuenta cada vez que se desencadena una operación de actualización de datos (ya sea por la programación o por una operación Ejecutar ahora), independientemente de si la operación se realiza correctamente o no. Si transcurre un número de ciclos (10, de forma predeterminada) sin solicitudes de conexión para el libro, la programación de actualización de datos se deshabilita debido a la inactividad.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|10|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<int >  
 Especifica cuánto tiempo conservar un registro histórico del procesamiento de la actualización de datos. Esta información aparece en las páginas del historial de actualización de datos que se mantienen para cada libro que usa la actualización de datos. También aparece en el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . El valor predeterminado es 365 días.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|365|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation \<cambiar >  
 Especifica el algoritmo de asignación basado en el estado que reenvía las solicitudes de conexión al servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que dispone de más CPU y recursos de memoria disponibles. Este es el algoritmo predeterminado de asignación. HealthBasedAllocation y RoundRobinBasedAllocation se excluyen mutuamente. Debe especificar uno u otro. Si establece ambos en false, se usará HealthBasedAllocation porque es el valor predeterminado. Si establece ambos en true, se obtiene un error de validación. La sintaxis para estos parámetros incluye especificar simplemente el nombre de parámetro, parameter:$true o parameter:$false.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<int >  
 Especifique el intervalo (en horas) para contar los eventos de carga y de conexión para calcular el ratio de carga frente a conexión. De forma predeterminada, el sistema calculará un nuevo ratio cada cuatro horas. Los valores válidos van de 1 a 24.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|4|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<int >  
 Especifica el ratio de eventos de carga con respecto a los eventos de conexión, que se usa como indicador del estado del servidor. El valor predeterminado es 20 por ciento.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|20|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>-MemoryDatabaseHoldLimit \<int >  
 Especifica cuántas horas permanece en memoria una base de datos inactiva para atender nuevas solicitudes de esos datos. Una base de datos activa se mantiene siempre en memoria mientras que se esté consultando, pero una vez que deja de estar activa, el sistema la mantendrá en memoria durante un período de tiempo adicional por si hay más solicitudes de esos datos. El valor predeterminado es 48 horas.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|48|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<int >  
 Especifica el número de segundos para recopilar estadísticas de respuesta de consultas antes de que se notifique como si fuera un evento de uso. El valor predeterminado es 300 segundos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|300|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-roundrobinallocation-switch"></a>-RoundRobinAllocation \<cambiar >  
 Especifica el algoritmo de asignación de round robin que reenvía las solicitudes de conexión al siguiente servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, alternando las solicitudes de forma equilibrada entre los servidores disponibles, independientemente de la carga del servidor. HealthBasedAllocation y RoundRobinBasedAllocation se excluyen mutuamente. Debe especificar uno u otro. Si establece ambos en false, se usará HealthBasedAllocation porque es el valor predeterminado. Si establece ambos en true, se obtiene un error de validación. La sintaxis para estos parámetros incluye especificar simplemente el nombre de parámetro, parameter:$true o parameter:$false.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount \<cadena >  
 Especifica el nombre de la aplicación de destino de una aplicación de Servicio de almacenamiento seguro que almacena una cuenta predefinida para ejecutar trabajos de actualización de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<int >  
 Especifica el número de días que se conserva el historial de datos de uso y las estadísticas de estado del servidor. El valor predeterminado es 365 días. Si se establece este valor en 0, se mantiene todo el historial indefinidamente.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|365|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<int >  
 Establece un límite superior que define un intercambio de solicitudes y respuestas esperado. El valor predeterminado es 3000 milisegundos. Cualquier solicitud que se complete entre 1000 y 3000 milisegundos se considera una respuesta esperada a los efectos de los informes.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|3000|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<int >  
 Establece un límite superior que define un intercambio de solicitudes y respuestas de ejecución prolongada.  El límite superior es de 10000 milisegundos. Cualquier solicitud que supere este límite entra dentro de la categoría Superada, que no tiene ningún umbral superior.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|10000|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<int >  
 Establece un límite superior que define un intercambio de solicitudes y respuestas rápido. El valor predeterminado es 1000 milisegundos. Cualquier solicitud que se complete entre 500 y 1000 milisegundos se considera una respuesta rápida a los efectos de los informes.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|1000|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<int >  
 Especifica una categoría de tiempos de respuesta que son demasiado pequeños para considerarse relevantes a los efectos de la recopilación de datos. La mayoría de las respuestas que entran en esta categoría son comunicaciones entre servidores. De forma predeterminada, este valor es 500 segundos. Cualquier solicitud que se complete entre 0 y 500 milisegundos es una solicitud trivial y se omite a los efectos del informe de errores.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|500|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<int >  
 Especifique el umbral (en días) para desencadenar una advertencia sobre un error para actualizar el archivo de datos usado por los informes del Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . De forma predeterminada, el sistema actualiza los datos de uso diariamente. El archivo Dashboard.xlsx de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , que es el origen de datos de los informes administrativos, se actualiza en la misma programación. Si el archivo .xlsx no se actualiza durante varios días, se desencadena una regla de estado que indica que el archivo está obsoleto. El valor predeterminado es 5 días. Los valores válidos van de 1 a 30.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|5|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 En este ejemplo se desactiva una característica de actualización de datos que se crea automáticamente y se administran las aplicaciones de destino del Servicio de almacenamiento seguro para almacenar credenciales de Windows arbitrarias. También establece la cuenta de actualización de datos desatendida de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una aplicación de destino predefinida.  
  
 Use Get-powerpivotserviceapplication para obtener una identidad válida.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 Este ejemplo especifica el algoritmo de asignación basado en el estado que reenvía las solicitudes de conexión el servidor que tiene la mayoría de los recursos disponibles.  
  
 Use Get-powerpivotserviceapplication para obtener una identidad válida.  
  
## <a name="example-3"></a>Ejemplo 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 En este ejemplo se muestra cómo establecer las horas inicial y final de un día laborable, que se usa como opción de programación para programar la actualización de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Las programaciones pueden especificar una opción de después del horario comercial para ejecutar la actualización de datos al final de un día laborable.  
  
 Use Get-powerpivotserviceapplication para obtener una identidad válida.  
  
  
