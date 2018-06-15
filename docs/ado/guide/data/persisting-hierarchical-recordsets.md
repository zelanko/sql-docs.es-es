---
title: Persistencia de conjuntos de registros jerárquicos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef907391ad15cb5dd4d58efb6268a0b1688274fb
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272524"
---
# <a name="persisting-hierarchical-recordsets"></a>Almacenar conjuntos de registros jerárquicos
Puede guardar un jerárquica **Recordset** a un archivo en formato ADTG o XML mediante una llamada a la [guardar](../../../ado/reference/ado-api/save-method.md) método. Sin embargo, se aplican dos limitaciones cuando se guarda jerárquica **Recordset**s en formato XML: no se puede guardar en XML si el jerárquica **Recordset** contiene las actualizaciones pendientes, y no se puede guardar un con parámetros jerárquica **conjunto de registros**.  
  
 Para obtener más información acerca del proveedor de forma de datos, vea [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) y [información general sobre el servicio de forma de datos para OLE DB](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
