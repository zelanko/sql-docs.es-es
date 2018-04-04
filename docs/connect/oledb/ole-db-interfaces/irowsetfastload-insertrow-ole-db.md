---
title: 'IRowsetFastLoad:: insertRow (OLE DB) | Documentos de Microsoft'
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4fbf689d2e31aee6b962254c61b90c210d0a0c6d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Agrega una fila al conjunto de filas de copia masiva. Para obtener ejemplos, vea [datos masiva copia masiva con IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) y [enviar datos de BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hAccessor*[in]  
 El identificador del descriptor de acceso que define los datos de fila para la copia masiva. El descriptor de acceso al que se hace referencia es un descriptor de acceso de fila, que enlaza la memoria propia del consumidor que contiene los valores de datos.  
  
 *pData*[in]  
 Puntero a la memoria propia del consumidor que contiene los valores de datos. Para obtener más información, vea [Estructuras DBBINDING](http://go.microsoft.com/fwlink/?LinkId=65955).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta. Los valores de estado enlazados de todas las columnas tienen el valor DBSTATUS_S_OK o DBSTATUS_S_NULL.  
  
 E_FAIL  
 Se ha producido un error. Hay información disponible sobre el error en las interfaces de error del conjunto de filas.  
  
 E_INVALIDARG  
 El argumento *pData* se estableció en un puntero NULL.  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL no pudo asignar memoria suficiente para completar la solicitud.  
  
 E_UNEXPECTED  
 Se llamó al método en un conjunto de filas de copia masiva previamente invalidado por la [IRowsetFastLoad:: Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) método.  
  
 DB_E_BADACCESSORHANDLE  
 El argumento *hAccessor* proporcionado por el consumidor no era válido.  
  
 DB_E_BADACCESSORTYPE  
 El descriptor de acceso especificado no era un descriptor de acceso de fila o no especificaba la memoria propia del consumidor.  
  
## <a name="remarks"></a>Comentarios  
 Error al convertir datos del consumidor a la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos para una columna provoca una devolución E_FAIL desde el controlador OLE DB para SQL Server. Se pueden transmitir datos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cualquier **InsertRow** método o solo en **confirmar** método. La aplicación de consumidor puede llamar al método **InsertRow** muchas veces con datos erróneos antes de recibir el aviso de que existe un error de conversión de tipo de datos. Dado que el método **Commit** asegura que el consumidor especifica correctamente todos los datos, este último puede utilizar el método **Commit** adecuadamente para validar los datos según sea necesario.  
  
 El controlador OLE DB para conjuntos de filas de copia de forma masiva de SQL Server son de solo escritura. El controlador OLE DB para SQL Server no expone ningún método que permita al consumidor consultar del conjunto de filas. Para finalizar el procesamiento, el consumidor puede liberar su referencia en la [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) interfaz sin llamar a la **confirmar** método. No hay recursos para obtener acceso a una fila insertada por el consumidor en el conjunto de filas y cambiar sus valores o quitarla individualmente del conjunto de filas.  
  
 Se da formato a las filas de copia masiva en el servidor para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las opciones que se hayan establecido para la conexión o sesión, como ANSI_PADDING, afectan al formato de fila. Esta opción está activada de forma predeterminada para las conexiones realizadas a través del controlador de OLE DB para SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
