---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 553f3aaaceae23944ae9b2d0be7d8129a22c0dd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112912"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener ejemplos, vea [datos masiva copia masiva con IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md) y [enviar datos de BLOB a SQL SERVER con IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 Se llamó al método en un conjunto de filas de copia masiva previamente invalidado por la **IRowsetFastLoad:: Commit** método.  
  
## <a name="remarks"></a>Notas  
 Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de filas copia masiva de proveedor de OLE DB de Native Client se comporta como un conjunto de filas de modo de actualización retrasada. Como el usuario inserta datos de fila mediante el conjunto de filas, filas insertadas se tratan del mismo modo que las inserciones en un conjunto de filas admite pendientes **IRowsetUpdate**.  
  
 El consumidor debe llamar a la **confirmar** método en el conjunto de filas de copia masiva para escribir las filas insertadas en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla de la misma manera que el **IRowsetUpdate:: Update** método se usa para enviar filas pendientes a un instancia de SQL Server.  
  
 Si el consumidor libera su referencia en el conjunto de filas de copia masiva sin llamar a la **confirmar** método, insertado todas las filas escritas anteriormente no se pierden.  
  
 El consumidor puede procesar por lotes las filas insertadas mediante una llamada a la **confirmar** método con el *fDone* establecido en FALSE. Cuando *fDone*está establecida en TRUE, el conjunto de filas deja de ser válido. Un conjunto de filas de copia masiva no válidos solo admite la **ISupportErrorInfo** interfaz y **IRowsetFastLoad:: Release** método.  
  
## <a name="see-also"></a>Vea también  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  