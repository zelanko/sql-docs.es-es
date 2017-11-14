---
title: "Método Execute21 (RDS) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b3a985a6bb9d9e50a3a6d6741a8f379abafc26af
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="execute21-method-rds"></a>Método Execute21 (RDS)
Ejecuta la solicitud y crea un conjunto de registros de ADO para su uso en ADO 2.1.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Una cadena que se utiliza para conectar con el proveedor OLE DB donde se enviará la solicitud para su ejecución. Si se especifica utilizando un controlador *HandlerString*, puede modificar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 La cadena identifica el controlador que se usarán con esta ejecución. La cadena consta de dos partes. La primera parte contiene el nombre (ProgID) del controlador que se usará. La segunda parte de la cadena contiene argumentos que se pasan al controlador. Cómo se interpreta la cadena de argumentos es específico del controlador. Las dos partes se separan mediante la primera instancia de una coma en la cadena (aunque puede contener comas adicionales en la cadena de argumentos). Los argumentos son opcionales.  
  
 *Cadena de consulta*  
 Un comando en el lenguaje de comandos admitido por el proveedor OLE DB identificado en la cadena de conexión. Para los proveedores basados en SQL, es posible que contenga un [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrucción de comandos, pero para los proveedores no son de SQL (por ejemplo, MSDataShape) no puede ser un [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrucción de consulta.  
  
 Además, si se está usando un controlador (y se recomienda encarecidamente que se usa un controlador), el controlador puede modificar o reemplazar el valor especificado aquí. Por ejemplo, el controlador normalmente reemplaza *QueryString* con una cadena de consulta mediante el archivo. ini. De forma predeterminada, se utiliza el archivo Msdfmap.ini.  
  
 *lMarshalOptions*  
 Se usa para establecer las opciones de serialización en el conjunto de filas/conjunto de registros que se devuelven.  
  
 *TableID*  
 Una variante de tipo VT_EMPTY o VT_BSTR. Si este valor es de tipo VT_EMPTY, se omite. Si es de tipo VT_BSTR, el conjunto de registros se crea mediante **adCmdTableDirect** con el valor especificado aquí y *QueryString* parámetro se ignora.  
  
 *lExecuteOptions*  
 Máscara de bits de opciones de ejecución:  
  
 1 =*ReadOnly* se abrirá el conjunto de registros mediante el uso de **adLockReadOnly**.  
  
 2 =*NoBatch* se abrirá el conjunto de registros mediante el uso de **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* el llamador garantiza que la información de parámetro para todos los parámetros se proporciona en *pParameters*.  
  
 8 =*GetInfo* información de parámetros para la consulta se obtenido del proveedor de OLE DB y se devolverá en el *pParameters* parámetro. No se ejecuta la consulta y no se devuelve ningún conjunto de registros.  
  
 16 = GetHiddenColumns se abrirá el conjunto de registros mediante el uso de **adLockBatchOptimistic** y las columnas ocultas se incluirán en el conjunto de registros.  
  
 Aunque *ReadOnly*, *NoBatch* y *GetHiddenColumns* son opciones mutuamente excluyentes, no es un error al establecer más de uno de ellos. Si se establecen varias opciones, *GetHiddenColumns* tiene prioridad sobre todas las demás opciones, seguidos por *ReadOnly*. Si no se especifica ninguna opción, de forma predeterminada, se abre el conjunto de registros mediante **adLockBatchOptimistic** pero las columnas ocultas no se incluyen en el conjunto de registros.  
  
 *pParameters*  
 Una variante que contiene una matriz segura de las definiciones de parámetro. Si el *GetInfo* se especificó la opción de *lExecuteOptions*, este parámetro se usa para devolver las definiciones de parámetro obtenidas del proveedor de OLE DB. En caso contrario, este parámetro puede estar vacío.  
  
## <a name="remarks"></a>Comentarios  
 El *HandlerString* parámetro puede ser null. Lo que ocurre en este caso depende de cómo esté configurado el servidor RDS. Una cadena de controlador de "MSDFMAP.handler" indica que se debe usar el controlador de Microsoft proporcionado (Msdfmap.dll). Una cadena de controlador de "MASDFMAP.handler,sample.ini" indica que se debe usar el controlador Msdfmap.dll y que se debe pasar el argumento "sample.ini" para el controlador. MSDFMAP.dll interpretará el argumento como una dirección que desea utilizar el sample.ini para comprobar las cadenas de conexión y consulta.  
  
> [!NOTE]
>  El **Execute21** método es una versión de la [Execute (método) (RDS)](../../../ado/reference/rds-api/execute-method-rds.md). Donde necesite usar la **Execute** método para comunicarse con ADO 2.1, la **Execute21** método puede llamarse en su lugar. Las capacidades de la **Execute** método en ADO 2.5 y versiones posterior son un superconjunto de las capacidades proporcionadas para el mismo método en ADO 2.1.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



