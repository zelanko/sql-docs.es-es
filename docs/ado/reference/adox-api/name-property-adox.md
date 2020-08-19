---
description: Name (propiedad, ADOX)
title: Name (propiedad, ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dbd0d9088ea39d604c53c462448ae1c94b3a9052
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439787"
---
# <a name="name-property-adox"></a>Name (propiedad, ADOX)
Indica el nombre del objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **cadena** .  
  
## <a name="remarks"></a>Observaciones  
 Los nombres no tienen que ser únicos dentro de una colección.  
  
 La propiedad **Name** es de lectura y escritura en objetos de [columna](../../../ado/reference/adox-api/column-object-adox.md), [grupo](../../../ado/reference/adox-api/group-object-adox.md), [clave](../../../ado/reference/adox-api/key-object-adox.md), [Índice](../../../ado/reference/adox-api/index-object-adox.md), [tabla](../../../ado/reference/adox-api/table-object-adox.md)y [usuario](../../../ado/reference/adox-api/user-object-adox.md) . La propiedad **Name** es de solo lectura en los objetos de [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md), [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md)y [vista](../../../ado/reference/adox-api/view-object-adox.md) .  
  
 En el caso de objetos de lectura/escritura (objetos de**columnas**, **grupos**, **claves**, **índices**, **tablas** y **usuarios** ), el valor predeterminado es una cadena vacía ("").  
  
> [!NOTE]
>  En el caso de las claves, esta propiedad es de solo lectura en objetos de **clave** ya anexados a una colección. En el caso de las tablas, esta propiedad es de solo lectura para los objetos de **tabla** ya anexados a una colección.  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
        [Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
        [Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)  
        [Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
        [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
        [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
        [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
