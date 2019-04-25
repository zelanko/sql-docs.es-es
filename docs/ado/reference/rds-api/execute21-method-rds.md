---
title: Método Execute21 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute21 method [RDS]
ms.assetid: 9f131c8d-1497-416d-8209-abb481c38f7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1b4608dde67f31067ed34f7c552ba866a2095ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469327"
---
# <a name="execute21-method-rds"></a>Método Execute21 (RDS)
Ejecuta la solicitud y crea un conjunto de registros ADO para su uso en ADO 2.1.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Execute21(ConnectionString As String, HandlerString As String, QueryString As String, lMarshalOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Cadena utilizada para conectarse al proveedor OLE DB donde se enviará la solicitud para su ejecución. Si se especifica utilizando un controlador *HandlerString*, puede modificar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 La cadena identifica el controlador que se usará con esta ejecución. La cadena contiene dos partes. La primera parte contiene el nombre (ProgID) del controlador que se usará. La segunda parte de la cadena contiene argumentos que se pasarán al controlador. Cómo se interpreta la cadena de argumentos es específico del controlador. Las dos partes se separan con la primera instancia de una coma en la cadena (aunque puede contener comas adicionales en la cadena de argumentos). Los argumentos son opcionales.  
  
 *QueryString*  
 Un comando en el lenguaje de comandos admitido por el proveedor OLE DB identificado en la cadena de conexión. Para los proveedores basados en SQL, es posible que contenga un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción de comando, pero para los proveedores que no son de SQL (por ejemplo, MSDataShape) no puede ser un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción de consulta.  
  
 Además, si se está usando un controlador (y se recomienda encarecidamente que se utiliza un controlador), el controlador puede modificar o reemplazar el valor especificado aquí. Por ejemplo, el controlador normalmente reemplaza *QueryString* con una cadena de consulta mediante el archivo. ini. De forma predeterminada, se usa el archivo Msdfmap.ini.  
  
 *lMarshalOptions*  
 Se usa para establecer las opciones de serialización en el conjunto de filas o conjunto de registros que se devuelven.  
  
 *TableID*  
 Una variante de tipo VT_EMPTY o VT_BSTR. Si este valor es de tipo VT_EMPTY, se omite. Si es de tipo VT_BSTR, se crea el conjunto de registros mediante **adCmdTableDirect** con el valor especificado aquí y *QueryString* parámetro se omite.  
  
 *lExecuteOptions*  
 Una máscara de bits de las opciones de ejecución:  
  
 1 =*ReadOnly* se abrirá el conjunto de registros mediante el uso de **adLockReadOnly**.  
  
 2 =*NoBatch* se abrirá el conjunto de registros mediante el uso de **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* el llamador garantiza que se proporciona información de parámetros para todos los parámetros en *pParameters*.  
  
 8 =*GetInfo* información de parámetros para la consulta se obtenido del proveedor OLE DB y se devolverá en la *pParameters* parámetro. No se ejecuta la consulta y no se devuelve ningún conjunto de registros.  
  
 16 = GetHiddenColumns se abrirá el conjunto de registros mediante el uso de **adLockBatchOptimistic** y las columnas ocultas se incluirán en el conjunto de registros.  
  
 Aunque *ReadOnly*, *NoBatch* y *GetHiddenColumns* son opciones mutuamente excluyentes, no es un error al establecer más de uno de ellos. Si se establecen varias opciones, *GetHiddenColumns* prevalece sobre todas las demás opciones, seguidos de *ReadOnly*. Si se especifica ninguna opción, de forma predeterminada, se abre el conjunto de registros mediante **adLockBatchOptimistic** pero no se incluyen las columnas ocultas en el conjunto de registros.  
  
 *pParameters*  
 Una variante que contiene una matriz segura de las definiciones de parámetro. Si el *GetInfo* especificó la opción de *lExecuteOptions*, este parámetro se usa para devolver las definiciones de parámetro obtenidas del proveedor OLE DB. En caso contrario, este parámetro puede estar vacío.  
  
## <a name="remarks"></a>Comentarios  
 El *HandlerString* parámetro puede ser null. Lo que ocurre en este caso depende de cómo se configura el servidor RDS. Una cadena de controlador de "MSDFMAP.handler" indica que se debe usar el controlador de Microsoft proporcionada (Msdfmap.dll). Una cadena de controlador de "MASDFMAP.handler,sample.ini" indica que se debe usar el controlador Msdfmap.dll y que se debe pasar el argumento "sample.ini" al controlador. MSDFMAP.dll interpretará el argumento como una dirección que desea utilizar el sample.ini para comprobar las cadenas de conexión y consulta.  
  
> [!NOTE]
>  El **Execute21** método es una versión de la [(RDS) del método Execute](../../../ado/reference/rds-api/execute-method-rds.md). Donde deberá usar el **Execute** método para comunicarse con ADO 2.1, la **Execute21** método se puede llamar en su lugar. Las capacidades de la **Execute** método ADO 2.5 y versiones posterior son un superconjunto de las capacidades proporcionadas para el mismo método en ADO 2.1.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


