---
title: Synchronize (método) (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39e5aef4700212c30d3e75d95ff2eaf40b2ed439
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815803"
---
# <a name="synchronize-method-rds"></a>Synchronize (método) (RDS)
Sincronizar el conjunto de registros determinado con la base de datos especificada por la cadena de conexión para su uso en ADO 2.5 y versiones posterior.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Cadena utilizada para conectarse al proveedor OLE DB donde se enviará la solicitud. Si se usa un controlador, el controlador puede modificar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 La cadena identifica el controlador que se usará con esta ejecución. La cadena contiene dos partes. La primera parte contiene el nombre (ProgID) del controlador que se usará. La segunda parte de la cadena contiene argumentos que se pasarán al controlador. Cómo se interpreta la cadena de argumentos es específico del controlador. Las dos partes se separan con la primera instancia de una coma en la cadena (aunque los argumentos de cadena pueden contener comas adicionales). Los argumentos son opcionales.  
  
 *lSynchronizeOptions*  
 Una máscara de bits de las opciones de sincronización.  
  
 1 =*UpdateTransact* las actualizaciones de la base de datos se encapsulan en una transacción. Si alguna de las actualizaciones se producen errores, se anula la transacción.  
  
 2 =*RefreshWithUpdate* causas fila los Estados que se devolverán cuando ninguna de ellas *actualizar* ni *RefreshConflicts* está establecido.  
  
 4 =*actualizar* se actualiza el conjunto de registros con datos actuales de la base de datos. Las actualizaciones pendientes no se insertan en la base de datos. Si no se establece este bit, no se actualiza el conjunto de registros y las actualizaciones pendientes se insertan en la base de datos.  
  
 8 =*RefreshConflicts* no se pudieron actualizar las filas con cambios pendientes. Se actualizan las filas que no se pudieron actualizar con datos actuales de la base de datos.  
  
 *ppRecordset*  
 Un puntero al conjunto de registros que se sincronizarán.  
  
 *pStatusArray*  
 Una variante que se usa para devolver una matriz segura de los Estados de fila para las filas afectadas por sincronizar. No se establece si se establece ninguna de las siguientes opciones de sincronización: *RefreshWithUpdate*, *actualizar* y *RefreshConflicts*.  
  
 *lcid*  
 El LCID utilizado para generar los errores que se devuelven en *pInformation*.  
  
 *pInformation*  
 Un puntero al error de la información devuelta por **Execute**. Si es NULL, no se devuelve ninguna información de error.  
  
## <a name="remarks"></a>Comentarios  
 El *HandlerString* parámetro puede ser null. ¿Qué ocurre en este caso depende de cómo se configura el servidor RDS. Una cadena de controlador de "MSDFMAP.handler" indica que se debe usar el controlador de Microsoft proporcionada (Msdfmap.dll). Una cadena de controlador de "MASDFMAP.handler,sample.ini" indica que se debe usar el controlador Msdfmap.dll y que se debe pasar el argumento "sample.ini" al controlador. MSDFMAP.dll interpretará, a continuación, el argumento como una dirección que desea utilizar el sample.ini para comprobar las cadenas de conexión y consulta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


