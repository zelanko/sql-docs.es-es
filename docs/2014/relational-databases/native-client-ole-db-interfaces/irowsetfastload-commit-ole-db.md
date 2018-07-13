---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 745282c1d1e8fa36c9d0a407ac32171304d05197
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417174"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener ejemplos, vea [masiva copia datos masiva con IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md) y [enviar datos BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *fDone*[in]  
 Si es FALSE, el conjunto de filas mantiene la validez y el consumidor puede usarlo para una inserción de filas adicional. Si es TRUE, el conjunto de filas pierde su validez y el consumidor no puede realizar ninguna inserción más.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ejecutó correctamente y todos los datos insertados se escribieron en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Se produjo un error específico del proveedor. Recupere la información de error para el texto de error específico del proveedor.  
  
 E_UNEXPECTED  
 Se llamó al método en un conjunto de filas de copia masiva previamente invalidado por el **IRowsetFastLoad:: Commit** método.  
  
## <a name="remarks"></a>Notas  
 Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de filas copia masiva de proveedor de OLE DB de Native Client se comporta como un conjunto de filas de modo de actualización retrasada. Como el usuario inserta datos de fila mediante el conjunto de filas, las filas insertadas se tratan del mismo modo que las inserciones en un conjunto de filas que admiten pendientes **IRowsetUpdate**.  
  
 El consumidor debe llamar a la **confirmar** método en el conjunto de filas de copia masiva para escribir las filas insertadas en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla en la misma manera que el **IRowsetUpdate:: Update** método se usa para enviar las filas pendientes a un instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar a la **confirmar** método, insertado en todas las filas escritas anteriormente no se pierden.  
  
 El consumidor puede procesar por lotes las filas insertadas llamando el **confirmar** método con el *fDone* argumento establecido en FALSE. Cuando *fDone*está establecida en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva no válidos solo admite la **ISupportErrorInfo** interfaz y **IRowsetFastLoad:: Release** método.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
