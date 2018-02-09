---
title: "Execute (método) (RDS) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be0dfb94d6681af706d75437143dcde28e63587d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="execute-method-rds"></a>Execute (método) (RDS)
Ejecuta la solicitud y crea un conjunto de registros de ADO para su uso en ADO 2.5 y versiones posteriores.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Una cadena que se utiliza para conectar con el proveedor OLE DB donde se enviará la solicitud para su ejecución. Si se especifica utilizando un controlador *HandlerString* puede modificar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 Una cadena de dos partes que identifica el controlador que se usarán con esta ejecución. La cadena consta de dos partes. La primera parte contiene el nombre (ProgID) del controlador que se usará. La segunda parte contiene argumentos que se pasan al controlador. Los detalles de cómo se interpreta la cadena de argumentos son específicos para cada controlador. Las dos partes se separan mediante la primera instancia de una coma en la cadena. La cadena de argumentos puede contener comas adicionales. Los argumentos son opcionales.  
  
 *QueryString*  
 Un comando en el lenguaje de comandos admitido por el proveedor OLE DB identificado en la cadena de conexión. Para los proveedores basados en SQL, *QueryString* puede contener una instrucción de comando de Transact-SQL, pero para los proveedores no son de SQL (por ejemplo, MSDataShape) no puede ser un [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrucción de consulta.  
  
 Si se utiliza un controlador, el controlador puede modificar o reemplazar el valor especificado aquí. Por ejemplo, el controlador normalmente reemplaza *QueryString* con una cadena de consulta mediante el archivo. ini. De forma predeterminada, se utiliza el archivo Msdfmap.ini.  
  
 *lFetchOptions*  
 Indica el tipo de recuperación asincrónica.  
  
 Para obtener más información, consulte [propiedad FetchOptions (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md).  
  
 *TableID*  
 A **Variant** de tipo VT_EMPTY o VT_BSTR. Si este valor es de tipo VT_EMPTY, se omite. Si es de tipo VT_BSTR, el conjunto de registros se crea mediante **adCmdTableDirect** y el valor especificado aquí y *QueryString* parámetro se ignora.  
  
 *lExecuteOptions*  
 Una máscara de bits de las opciones de ejecución:  
  
 1 =*ReadOnly* se abrirá el conjunto de registros mediante el uso de **adLockReadOnly**.  
  
 2 =*NoBatch* se abrirá el conjunto de registros mediante el uso de **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* el llamador garantiza que la información de parámetro para todos los parámetros se proporciona en *pParameters*.  
  
 8 =*GetInfo* información de parámetros para la consulta se obtenido del proveedor de OLE DB y se devolverá en el *pParameters* parámetro. No se ejecuta la consulta y no se devuelve ningún conjunto de registros.  
  
 16 =*GetHiddenColumns* se abrirá el conjunto de registros mediante el uso de **adLockBatchOptimistic** y las columnas ocultas se incluirán en el conjunto de registros.  
  
 *ReadOnly*, *NoBatch* y *GetHiddenColumns* son opciones mutuamente excluyentes; sin embargo, no genera un error para establecer más de uno de ellos. Si se establecen varias opciones, *GetHiddenColumns* tiene prioridad sobre todos los demás, seguido de *ReadOnly*. Si no se especifica ninguna opción, de forma predeterminada, se abre el conjunto de registros mediante **adLockBatchOptimistic** y las columnas ocultas no se incluyen en el conjunto de registros.  
  
 *pParameters*  
 A **Variant** que contiene una matriz segura de las definiciones de parámetro. Si el *GetInfo* se especificó la opción de *lExecuteOptions*, este parámetro se usa para devolver las definiciones de parámetro obtenidas del proveedor de OLE DB. En caso contrario, este parámetro puede estar vacío.  
  
 *lcid*  
 El LCID utilizado para generar los errores que se devuelven en *pInformation*.  
  
 *pInformation*  
 Un puntero al error de la información devuelto por la ejecución. Si es NULL, no se devuelve ninguna información de error.  
  
## <a name="remarks"></a>Comentarios  
 El *HandlerString* parámetro puede ser null. ¿Qué ocurre en este caso depende de cómo esté configurado el servidor RDS. Una cadena de controlador de "MSDFMAP.handler" indica que se debe usar el controlador de Microsoft proporcionado (Msdfmap.dll). Una cadena de controlador de "MASDFMAP.handler,sample.ini" indica que se debe usar el controlador Msdfmap.dll y que se debe pasar el argumento "sample.ini" para el controlador. MSDFMAP.dll interpretará el argumento como una dirección que desea utilizar el sample.ini para comprobar las cadenas de conexión y consulta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


