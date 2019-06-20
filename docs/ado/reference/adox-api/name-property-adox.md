---
title: Nombre (propiedad, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f7b61dd2c1dc5899852234d23148969dad9c3dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706376"
---
# <a name="name-property-adox"></a>Name (propiedad, ADOX)
Indica el nombre del objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor.  
  
## <a name="remarks"></a>Comentarios  
 Nombres no tienen que ser único dentro de una colección.  
  
 El **nombre** propiedad es de lectura/escritura en [columna](../../../ado/reference/adox-api/column-object-adox.md), [grupo](../../../ado/reference/adox-api/group-object-adox.md), [clave](../../../ado/reference/adox-api/key-object-adox.md), [índice](../../../ado/reference/adox-api/index-object-adox.md), [ Tabla](../../../ado/reference/adox-api/table-object-adox.md), y [usuario](../../../ado/reference/adox-api/user-object-adox.md) objetos. El **nombre** propiedad es de solo lectura en [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md), [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md), y [vista](../../../ado/reference/adox-api/view-object-adox.md) objetos.  
  
 Para los objetos de lectura/escritura (**columna**, **grupo**, **clave**, **índice**, **tabla** y  **Usuario** objetos), el valor predeterminado es una cadena vacía ("").  
  
> [!NOTE]
>  Para las claves, esta propiedad es de solo lectura en **clave** ya anexados a una colección de objetos. Para las tablas, esta propiedad es de solo lectura para **tabla** ya anexados a una colección de objetos.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
