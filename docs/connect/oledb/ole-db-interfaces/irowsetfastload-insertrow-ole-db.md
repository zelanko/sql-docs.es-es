---
title: 'IRowsetFastLoad:: insertRow (OLE DB) | Microsoft Docs'
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 780110a1d7a606a9277ae10fbd9260a5f587f6d7
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030892"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Agrega una fila al conjunto de filas de copia masiva. Para obtener ejemplos, vea [masiva copia datos masiva con IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) y [enviar datos BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 MSOLEDBSQL no pudo asignar la memoria suficiente para completar la solicitud.  
  
 E_UNEXPECTED  
 Se llamó al método en un conjunto de filas de copia masiva previamente invalidado por el método [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) .  
  
 DB_E_BADACCESSORHANDLE  
 El argumento *hAccessor* proporcionado por el consumidor no era válido.  
  
 DB_E_BADACCESSORTYPE  
 El descriptor de acceso especificado no era un descriptor de acceso de fila o no especificaba la memoria propia del consumidor.  
  
## <a name="remarks"></a>Notas  
 Un error al convertir los datos del consumidor al tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una columna hace que el controlador OLE DB para SQL Server devuelva E_FAIL. Los datos se pueden transmitir a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cualquier método **InsertRow** o solo en el método **Commit**. La aplicación de consumidor puede llamar al método **InsertRow** muchas veces con datos erróneos antes de recibir el aviso de que existe un error de conversión de tipo de datos. Dado que el método **Commit** asegura que el consumidor especifica correctamente todos los datos, este último puede utilizar el método **Commit** adecuadamente para validar los datos según sea necesario.  
  
 El controlador OLE DB para los conjuntos de filas de copia masiva SQL Server son de solo escritura. El controlador OLE DB para SQL Server no expone ningún método que permita al consumidor consultar del conjunto de filas. Para finalizar el procesamiento, el consumidor puede liberar su referencia en la interfaz [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) sin llamar al método **Commit**. No hay recursos para obtener acceso a una fila insertada por el consumidor en el conjunto de filas y cambiar sus valores o quitarla individualmente del conjunto de filas.  
  
 Se da formato a las filas de copia masiva en el servidor para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las opciones que se hayan establecido para la conexión o sesión, como ANSI_PADDING, afectan al formato de fila. Esta opción está activada de forma predeterminada para las conexiones realizadas a través del controlador OLE DB para SQL Server.  
  
## <a name="see-also"></a>Ver también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
