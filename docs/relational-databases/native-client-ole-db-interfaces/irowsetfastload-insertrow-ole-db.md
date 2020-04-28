---
title: IRowsetFastLoad::InsertRow (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c178f2e948e27b964b04f62508ec35038b204576
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307289"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Agrega una fila al conjunto de filas de copia masiva. Para ver ejemplos, consulte [Copiar datos de forma masiva mediante IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) y [Enviar datos BLOB a SQL SERVER mediante IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 Puntero a la memoria propia del consumidor que contiene los valores de datos. Para obtener más información, vea [Estructuras DBBINDING](https://go.microsoft.com/fwlink/?LinkId=65955).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta. Los valores de estado enlazados de todas las columnas tienen el valor DBSTATUS_S_OK o DBSTATUS_S_NULL.  
  
 E_FAIL  
 Se produjo un error. Hay información disponible sobre el error en las interfaces de error del conjunto de filas.  
  
 E_INVALIDARG  
 El argumento *pData* se estableció en un puntero NULL.  
  
 E_OUTOFMEMORY  
 SQLNCLI11 no ha podido asignar la memoria suficiente para completar la solicitud.  
  
 E_UNEXPECTED  
 Se ha llamado al método en un conjunto de filas de copia masiva previamente invalidado por el método [IRowsetFastLoad::Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md).  
  
 DB_E_BADACCESSORHANDLE  
 El argumento *hAccessor* proporcionado por el consumidor no era válido.  
  
 DB_E_BADACCESSORTYPE  
 El descriptor de acceso especificado no era un descriptor de acceso de fila o no especificaba la memoria propia del consumidor.  
  
## <a name="remarks"></a>Observaciones  
 Un error al convertir los datos del consumidor al tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una columna hace que el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelva E_FAIL. Los datos se pueden transmitir a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en cualquier método **InsertRow** o solo en el método **Commit**. La aplicación de consumidor puede llamar al método **InsertRow** muchas veces con datos erróneos antes de recibir el aviso de que existe un error de conversión de tipo de datos. Dado que el método **Commit** asegura que el consumidor especifica correctamente todos los datos, este último puede utilizar el método **Commit** adecuadamente para validar los datos según sea necesario.  
  
 Los conjuntos de filas de copia masiva del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client son de solo escritura. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no expone ningún método que permita al consumidor consultar el conjunto de filas. Para finalizar el procesamiento, el consumidor puede liberar su referencia en la interfaz [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) sin llamar al método **Commit**. No hay recursos para obtener acceso a una fila insertada por el consumidor en el conjunto de filas y cambiar sus valores o quitarla individualmente del conjunto de filas.  
  
 Se da formato a las filas de copia masiva en el servidor para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las opciones que se hayan establecido para la conexión o sesión, como ANSI_PADDING, afectan al formato de fila. Esta opción está activada de forma predeterminada para las conexiones realizadas a través del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
