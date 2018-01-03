---
title: "Método Synchronize21 (RDS) | Documentos de Microsoft"
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f48789fef088affdfa664ead4da2bd379aa51b7
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="synchronize21-method-rds"></a>Método Synchronize21 (RDS)
Sincronizar el conjunto de registros determinado con la base de datos especificada por la cadena de conexión para su uso con ADO 2.1.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Una cadena que se utiliza para conectar con el proveedor OLE DB donde se enviará la solicitud. Si se utiliza un controlador, el controlador puede modificar o reemplazar la cadena de conexión.  
  
 *HandlerString*  
 La cadena identifica el controlador que se usarán con esta ejecución. La cadena consta de dos partes. La primera parte contiene el nombre (ProgID) del controlador que se usará. La segunda parte de la cadena contiene argumentos que se pasan al controlador. Cómo se interpreta la cadena de argumentos es específico del controlador. Las dos partes se separan mediante la primera instancia de una coma en la cadena. La cadena de argumentos puede contener comas adicionales. Los argumentos son opcionales.  
  
 *lSynchronizeOptions*  
 Una máscara de bits de las opciones de sincronización.  
  
 1 =*UpdateTransact* las actualizaciones de la base de datos se encapsulan en una transacción. Si no se produce alguna de las actualizaciones, se anula la transacción.  
  
 2 =*RefreshWithUpdate* causas fila estados se devolverá cuando ninguna de ellas *actualizar* ni *RefreshConflicts* se establece.  
  
 4 =*actualizar* el conjunto de registros se actualiza con los datos actuales de la base de datos. Las actualizaciones pendientes no se insertan en la base de datos. Si este bit no está establecido, no se actualiza el conjunto de registros y las actualizaciones pendientes se insertan en la base de datos.  
  
 8 =*RefreshConflicts* no se pudieron actualizar las filas con cambios pendientes. Las filas que no se pudo actualizar se actualizan con los datos actuales de la base de datos.  
  
 *ppRecordset*  
 Un puntero a un puntero al conjunto de registros que se sincronizarán.  
  
 *pStatusArray*  
 Una variante que se usa para devolver una matriz segura de Estados de fila para las filas afectadas por sincronizar. No se establece si se establece ninguna de las siguientes opciones de sincronización: *RefreshWithUpdate*, *actualizar* y *RefreshConflicts*.  
  
## <a name="remarks"></a>Comentarios  
 El *HandlerString* parámetro puede ser null. ¿Qué ocurre en este caso depende de cómo esté configurado el servidor RDS. Una cadena de controlador de "MSDFMAP.handler" indica que se debe usar el controlador de Microsoft proporcionado (Msdfmap.dll). Una cadena de controlador de "MASDFMAP.handler,sample.ini" indica que se debe usar el controlador Msdfmap.dll y que se debe pasar el argumento "sample.ini" para el controlador. MSDFMAP.dll interpretará, a continuación, el argumento como una dirección que desea utilizar el sample.ini para comprobar las cadenas de conexión y consulta.  
  
> [!NOTE]
>  El **Synchronize21** método es simplemente una versión de la [método sincronizar (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md). Donde necesite usar la **sincronizar** método para comunicarse con ADO 2.1, la **Synchronize21** método puede llamarse en su lugar. Las capacidades de la **sincronizar** método en ADO 2.5 y versiones posterior son un superconjunto de las capacidades proporcionadas para el mismo método en ADO 2.1.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


