---
title: IRowsetFastLoad (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e6983eaccf1a934a318c69e72ebdfebf17d2ad9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224723"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener ejemplos, vea [masiva copia datos masiva con IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md) y [enviar datos BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 Se ha llamado al método en un conjunto de filas de copia masiva previamente invalidado por el método **IRowsetFastLoad::Commit**.  
  
## <a name="remarks"></a>Comentarios  
 Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de filas copia masiva de proveedor de OLE DB de Native Client se comporta como un conjunto de filas de modo de actualización retrasada. A medida que el usuario inserta los datos de fila a través del conjunto de filas, las filas insertadas reciben el mismo trato que las inserciones pendientes en un conjunto de filas que admite **IRowsetUpdate**.  
  
 El consumidor debe llamar al método **Commit** en el conjunto de filas de copia masiva para escribir las filas insertadas en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del mismo modo en que se usa el método **IRowsetUpdate::Update** para enviar las filas pendientes a una instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar al método **Commit**, se perderán todas las filas insertadas que no se hayan escrito previamente.  
  
 El consumidor puede procesar por lotes las filas insertadas mediante una llamada al método **Commit** con el argumento *fDone* establecido en FALSE. Cuando *fDone* se establece en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva que no es válido solo admite la interfaz **ISupportErrorInfo** y el método **IRowsetFastLoad::Release**.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
