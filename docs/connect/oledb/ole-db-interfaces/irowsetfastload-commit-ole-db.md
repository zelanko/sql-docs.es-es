---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Documentos de Microsoft'
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8f4baa2339105e8dac65c29e5efc35663b7c4b8d
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689858"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener ejemplos, vea [datos masiva copia masiva con IRowsetFastLoad &#40;OLE DB&#41; ](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) y [enviar datos de BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fDone*[in]  
 Si es FALSE, el conjunto de filas mantiene la validez y el consumidor puede usarlo para una inserción de filas adicional. Si es TRUE, el conjunto de filas pierde su validez y el consumidor no puede realizar ninguna inserción más.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ejecutó correctamente y todos los datos insertados se escribieron en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Se produjo un error específico del proveedor. Recupere la información de error para el texto de error específico del proveedor.  
  
 E_UNEXPECTED  
 Se llamó al método en un conjunto de filas de copia masiva previamente invalidado por la **IRowsetFastLoad:: Commit** método.  
  
## <a name="remarks"></a>Notas  
 Un controlador de OLE DB para filas de copia masiva de SQL Server se comporta como un conjunto de filas de modo de actualización retrasada. Como el usuario inserta datos de fila mediante el conjunto de filas, filas insertadas se tratan del mismo modo que las inserciones en un conjunto de filas admite pendientes **IRowsetUpdate**.  
  
 El consumidor debe llamar a la **confirmar** método en el conjunto de filas de copia masiva para escribir las filas insertadas en la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla de la misma manera que el **IRowsetUpdate:: Update** método se usa para enviar filas pendientes a un instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar a la **confirmar** método, insertado todas las filas escritas anteriormente no se pierden.  
  
 El consumidor puede procesar por lotes las filas insertadas mediante una llamada a la **confirmar** método con el *fDone* establecido en FALSE. Cuando *fDone*está establecida en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva no válidos solo admite la **ISupportErrorInfo** interfaz y **IRowsetFastLoad:: Release** método.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
