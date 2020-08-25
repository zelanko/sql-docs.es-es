---
description: SortOrder (propiedad, ADOX)
title: SortOrder (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::SortOrder
- _Column::PutSortOrder
- _Column::put_SortOrder
- _Column::get_SortOrder
- _Column::GetSortOrder
helpviewer_keywords:
- SortOrder property [ADOX]
ms.assetid: 04510b19-9cb2-4895-b23b-f7790123eb04
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f0af0f636513c3648755eb1d0c905e7a76ef9ee
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769374"
---
# <a name="sortorder-property-adox"></a>SortOrder (propiedad, ADOX)
Indica la secuencia de ordenación de la columna (solo columnas de índice).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un valor **Long** que puede ser una de las constantes [SortOrderEnum](./sortorderenum.md) . El valor predeterminado es **adSortAscending**.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad solo se aplica a los objetos de [columna](./column-object-adox.md) de la colección [Columns](./columns-collection-adox.md) de un [Índice](./index-object-adox.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Colección de columnas (ADOX)](./columns-collection-adox.md)   
 [Objeto Index (ADOX)](./index-object-adox.md)