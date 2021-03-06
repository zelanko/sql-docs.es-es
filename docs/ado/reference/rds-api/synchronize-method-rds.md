---
description: Synchronize (método) (RDS)
title: Synchronize (método) (RDS) | Microsoft Docs
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e903d5a3d80af26e9fd1ca36920e5b91adb06b1f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724169"
---
# <a name="synchronize-method-rds"></a>Synchronize (método) (RDS)
Sincronizar el conjunto de registros dado con la base de datos especificada por la cadena de conexión para su uso en ADO 2,5 y versiones posteriores.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Cadena que se usa para conectar con el proveedor de OLE DB donde se enviará la solicitud. Si se usa un controlador, el controlador puede editar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 La cadena identifica el controlador que se va a utilizar con esta ejecución. La cadena contiene dos partes. La primera parte contiene el nombre (ProgID) del controlador que se va a usar. La segunda parte de la cadena contiene los argumentos que se van a pasar al controlador. La forma en que se interpreta la cadena arguments es específica del controlador. Las dos partes se separan mediante la primera instancia de una coma de la cadena (aunque la cadena arguments puede contener comas adicionales). Los argumentos son opcionales.  
  
 *lSynchronizeOptions*  
 Máscara de bits de las opciones de sincronización.  
  
 1 =*UpdateTransact* las actualizaciones de la base de datos se ajustan en una transacción. La transacción se anula si se produce un error en alguna de las actualizaciones.  
  
 2 =*RefreshWithUpdate* hace que se devuelvan los Estados de fila cuando no se establece ninguna *actualización* ni *RefreshConflicts* .  
  
 4 = la*actualización* del conjunto de registros se actualiza con los datos actuales de la base de datos. Las actualizaciones pendientes no se insertan en la base de datos. Si no se establece este bit, el conjunto de registros no se actualiza y las actualizaciones pendientes se insertan en la base de datos.  
  
 8 =*RefreshConflicts* las filas con cambios pendientes no se pueden actualizar. Las filas que no se pudieron actualizar se actualizan con los datos actuales de la base de datos.  
  
 *ppRecordset*  
 Puntero al conjunto de registros que se va a sincronizar.  
  
 *pStatusArray*  
 Variant que se usa para devolver una matriz segura de Estados de fila para las filas afectadas por la sincronización. No se establece si no se establece ninguna de las siguientes opciones de sincronización: *RefreshWithUpdate*, *Refresh* y *RefreshConflicts*.  
  
 *lcid*  
 LCID que se usa para compilar los errores que se devuelven en *pInformation*.  
  
 *pInformation*  
 Un puntero a un error de información devuelto por **Execute**. Si es NULL, no se devuelve información de error.  
  
## <a name="remarks"></a>Observaciones  
 El parámetro *HandlerString* puede ser null. Lo que sucede en este caso depende de cómo esté configurado el servidor RDS. Una cadena de controlador de "MSDFMAP. handler" indica que se debe usar el controlador proporcionado por Microsoft (Msdfmap.dll). Una cadena de controlador de "MASDFMAP. handler, sample.ini" indica que se debe usar el controlador de Msdfmap.dll y que el argumento "sample.ini" se debe pasar al controlador. A continuación, Msdfmap.dll interpretará el argumento como una dirección para usar el sample.ini para comprobar las cadenas de conexión y de consulta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)