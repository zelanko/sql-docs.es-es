---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Documentos de Microsoft'
description: IRowsetFastLoad::Commit (OLE DB)
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
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93e3b1a7bf97da890e77e3c51d6c1f5bc6f67ee0
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
## <a name="remarks"></a>Comentarios  
 Un controlador de OLE DB para filas de copia masiva de SQL Server se comporta como un conjunto de filas de modo de actualización retrasada. Como el usuario inserta datos de fila mediante el conjunto de filas, filas insertadas se tratan del mismo modo que las inserciones en un conjunto de filas admite pendientes **IRowsetUpdate**.  
  
 El consumidor debe llamar a la **confirmar** método en el conjunto de filas de copia masiva para escribir las filas insertadas en la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla de la misma manera que el **IRowsetUpdate:: Update** método se usa para enviar filas pendientes a un instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar a la **confirmar** método, insertado todas las filas escritas anteriormente no se pierden.  
  
 El consumidor puede procesar por lotes las filas insertadas mediante una llamada a la **confirmar** método con el *fDone* establecido en FALSE. Cuando *fDone*está establecida en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva no válidos solo admite la **ISupportErrorInfo** interfaz y **IRowsetFastLoad:: Release** método.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
