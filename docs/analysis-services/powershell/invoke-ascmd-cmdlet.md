---
title: Cmdlet Invoke-ASCmd | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf570da0e7be70fda804a3f17d11f6c8498c1605
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027815"
---
# <a name="invoke-ascmd-cmdlet"></a>Cmdlet Invoke-ASCmd
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Permite a un administrador de bases de datos ejecutar instrucciones de script XMLA, expresiones multidimensionales (MDX), instrucciones de extensiones de minería de datos (DMX) o scripts de lenguaje de script de modelo tabular (TMSL).  
  
 TMSL solo se admite en modo de servidor tabular en una instancia de Analysis Services de SQL Server 2016.  
  
 Si desea crear bases de datos u otros objetos, este es el cmdlet que usaría, con un archivo de entrada de script.  
  
## <a name="syntax"></a>Sintaxis  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 El cmdlet Invoke-ASCmd puede ejecutar las consultas o los scripts contenidos en los archivos de entrada.  
  
 Para XMLA, se admiten los siguientes comandos: Alter, Backup, Batch, BeginTransaction, Cancel, ClearCache, CommitTransaction, Create, Delete, DesignAggregations, Drop, Insert, Lock, MergePartitions, NotifyTableChange, Process, Restore, RollbackTransaction, Statement (que se usan para ejecutar consultas MDX e instrucciones DMX), Subscribe, Synchronize, Unlock, Update, UpdateCells.  
  
 Para TMSL: Alter, Create, Delete, MergePartitions, Process, Update.  
  
 Este cmdlet admite el parámetro –Credential, que se puede usar si configuró la instancia de Analysis Services para el acceso HTTP. El parámetro –Credential toma un objeto PSCredential que proporciona una identidad de usuario de Windows. A continuación, IIS suplantará a este usuario al conectarse a Analysis Services. La identidad debe tener permisos de administrador del sistema en la instancia de Analysis Services para ejecutar el script.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-query-string"></a>: Realiza una consulta \<cadena >  
 Especifica el script, la consulta o la instrucción reales directamente en la línea de comandos en lugar de hacerlo en un archivo. También puede especificar una consulta como entrada de la canalización. Es necesario especificar un valor para los parámetros **–InputFile** o **–Query** al usar **Invoke-AsCmd**.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|True (ByValue)|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-inputfile-string"></a>-InputFile \<cadena >  
 Identifica el archivo que contiene el script XMLA, la consulta MDX, la instrucción DMX o el script TMSL (en JSON). Es necesario especificar un valor para los parámetros **–InputFile** o **–Query** al usar **Invoke-AsCmd**.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-server-string"></a>-Server \<cadena >  
 Especifica la instancia de Analysis Services a la que el cmdlet se conectará y ejecutará. Si no se proporciona un nombre de servidor, se establecerá una conexión al host local. Para las instancias predeterminadas, especifique solo el nombre del servidor. Para las instancias con nombre, utilice el formato nombreDeServidor\nombreDeInstancia. En las conexiones HTTP, utilice el formato http[s]://server[:port]/virtualdirectory/msmdpump.dll.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|localhost|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-database-string"></a>-Base de datos \<cadena >  
 Especifica la base de datos en la que se ejecutará una consulta MDX o una instrucción DMX. El parámetro database se omite cuando el cmdlet ejecuta un script XMLA, ya que el script XMLA incluye el nombre de la base de datos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Especifica un objeto PSCredential que proporciona el nombre de usuario y contraseña de Windows. Especifique este parámetro solo si la instancia de Analysis Services está configurada para el acceso HTTP con autenticación básica. Para las conexiones nativas que usan seguridad integrada, este parámetro se omite.  
  
 Si este parámetro está presente, las credenciales que proporcione se anexan a la cadena de conexión. IIS suplantará esta identidad de usuario al conectarse a Analysis Services. Si no se especifica ninguna credencial, se usará la cuenta predeterminada de Windows del usuario que ejecuta la herramienta.  
  
 Para usar este parámetro, cree primero un objeto PSCredential con Get-Credential para especificar el nombre de usuario y la contraseña (por ejemplo, `$Cred=Get-Credential “adventure-works\admin”`. Después, puede canalizar este objeto al parámetro -Credential `(-Credential:$Cred`).  
  
   Para más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|True (ByValue)|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<int >  
 Especifica el número de segundos antes de que se agote el tiempo de espera de la conexión a la instancia de Analysis Services. El tiempo de espera debe ser un entero comprendido entre 0 y 65534. Si se especifica 0, los intentos de conexión no tienen tiempo de espera.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|30|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<int >  
 Especifica el número de segundos que tienen que transcurrir antes de que las consultas agoten el tiempo de espera. Si no se especifica ningún valor de tiempo de espera, las consultas no agotan el tiempo de espera. El tiempo de espera debe ser un entero comprendido entre 1 y 65535.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|30|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-variable-string"></a>-Variable \<string [] >  
 Especifica variables de scripting adicionales. Cada variable es un par de nombre y valor. Si el valor contiene caracteres de control o espacios incrustados, debe ponerse entre comillas dobles. Use una matriz de PowerShell para especificar varias variables y sus valores.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-tracefile-string"></a>-TraceFile \<cadena >  
 Identifica un archivo que recibe eventos de seguimiento de Analysis Services al ejecutar el script XMLA, la consulta MDX o la instrucción DMX. Si ya existe el archivo, se sobrescribe automáticamente (a excepción de los archivos de seguimiento que se crean con configuración de los parámetros the -TraceLevel:Duration y –TraceLevel:DurationResult). Los nombres de archivo que contienen espacios deben ir entre comillas (" "). Si el nombre de archivo no es válido, se genera un mensaje de error.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat \<cadena >  
 Especifica el formato de archivo del parámetro –TraceFile (si se ha especificado dicho parámetro). Las opciones disponibles son texto o csv. El valor predeterminado es “csv".  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|csv|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter \<cadena >  
 Especifica qué carácter usar como delimitador del archivo de seguimiento al especificar csv como formato del archivo de seguimiento. El valor predeterminado es | (barra vertical).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<int >  
 Especifica el número de segundos que el motor de Analysis Services espera antes de finalizar el seguimiento (si especifica el parámetro –TraceFile). Se considera que el seguimiento ha terminado si no se han registrado mensajes relacionados con él durante el período de tiempo especificado. El valor predeterminado del tiempo de espera de seguimiento es de 5 segundos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|5|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-tracelevel-traceleveloption"></a>-TraceLevel \<TraceLevelOption >  
 Especifica qué datos se recopilan y registran en el archivo de seguimiento. Los valores posibles son High, Medium, Low, Duration y DurationResult.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|Alta|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|PSObject|  
|Resultados|String|  
  
## <a name="example-1-xmla-input-file"></a>Ejemplo 1 (archivo de entrada de XMLA)  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 Este comando ejecuta un script XMLA que devuelve la lista de conexiones activas en el servidor. El archivo DiscoverConnections.xmla contiene el script XMLA siguiente:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>Ejemplo 2 (archivo de entrada de TMSL)  
 Este ejemplo es idéntico al primero, excepto por el script que es TMSL (JSON) y requiere una instancia tabular de SQL Server 2016. Puede generar un script TMSL en SQL Server Management Studio.  
  
 Si tiene varias instancias y la instancia tabular es una instancia con nombre, recuerde establecer el nombre del servidor:  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>Ejemplo 3 (consulta)  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 La consulta de detección XMLA devuelve los orígenes de datos disponibles de Analysis Services y la información necesaria para conectarse a ellos. Los resultados están en XML. Para mejorar la legibilidad, puede canalizar la salida a un archivo XML (por ejemplo, anexe `| Out-file C:\Results\XMLAQueryOutput.xml` al comando) y ver los resultados en el explorador u otra aplicación compatible con XML estructurado.  
  
  
  
