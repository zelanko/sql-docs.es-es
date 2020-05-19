---
title: Creación, modificación y eliminación de índices XML selectivos secundarios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b563b2c786f7ac1f9031dbddc4c5f343ebf688e9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717125"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>Crear, modificar y quitar índices XML selectivos secundarios
  Describe cómo crear un nuevo índice XML selectivo secundario, o cómo modificar o quitar un índice XML selectivo secundario existente.  
  
##  <a name="creating-a-secondary-selective-xml-index"></a><a name="create"></a> Crear un índice XML selectivo secundario  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>Crear un índice XML selectivo secundario  
 **Crear un índice XML selectivo secundario con Transact-SQL**  
 Crear un índice XML selectivo secundario llamando a la instrucción CREATE SELECTIVE XML INDEX. Para obtener más información, vea [crear índice XML &#40;índices XML selectivos&#41;] (~/t-SQL/statements/Create-XML-index-Selective-XML-Indexes.  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se crea un índice XML selectivo secundario en la ruta de acceso `'pathabc'`. La ruta de acceso del índice se identifica mediante el nombre que se ha especificado cuando se creó con la instrucción CREATE SELECTIVE XML INDEX. Para obtener más información, vea [CREAR ÍNDICE XML SELECTIVO &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql).  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="altering-a-secondary-selective-xml-index"></a><a name="alter"></a> Alterar un índice XML selectivo secundario  
 La instrucción ALTER no se admite para los índices XML selectivos secundarios. Para cambiar un índice XML secundario selectivo, quite el índice existente y vuelva a crearlo.  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>Modificar un índice XML selectivo secundario  
 **Modificar un índice XML selectivo secundario con Transact-SQL**  
 1.  Quite el índice XML selectivo secundario existente llamando a la instrucción DROP INDEX. Para obtener más información, vea [DROP INDEX &#40;índices XML selectivos&#41;](../indexes/indexes.md).  
  
2.  Vuelva a crear el índice con las opciones deseadas llamando a la instrucción CREATE XML INDEX. Para obtener más información, vea [crear índice XML &#40;índices XML selectivos&#41;] (~/t-SQL/statements/Create-XML-index-Selective-XML-Indexes.  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se cambia un índice XML selectivo secundario quitándolo y volviéndolo a crear.  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="dropping-a-secondary-selective-xml-index"></a><a name="drop"></a> Quitar un índice XML selectivo secundario  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>Quitar un índice XML selectivo secundario  
 **Quitar un índice XML selectivo secundario con Transact-SQL**  
 Quitar un índice XML selectivo secundario llamando a la instrucción DROP INDEX. Para obtener más información, vea [DROP INDEX &#40;índices XML selectivos&#41;](../indexes/indexes.md).  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se muestra una instrucción DROP INDEX.  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>Consulte también  
 [Índices XML selectivos &#40;SXI&#41;](selective-xml-indexes-sxi.md)  
  
  
