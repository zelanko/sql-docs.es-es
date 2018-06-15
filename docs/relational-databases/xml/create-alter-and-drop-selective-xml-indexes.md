---
title: Creación, modificación y eliminación de índices XML selectivos | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c3d819ce2d83df4be1337129b9425dfe0c21498f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33011702"
---
# <a name="create-alter-and-drop-selective-xml-indexes"></a>Crear, modificar y quitar índices XML selectivos
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Describe cómo crear un nuevo índice XML selectivo, o cómo modificar o quitar un índice XML selectivo existente.  
  
 Para obtener más información sobre los índices XML selectivos, vea [Índices XML selectivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
##  <a name="create"></a> Crear un índice XML selectivo  
  
### <a name="how-to-create-a-selective-xml-index"></a>Crear un índice XML selectivo  
 **Crear un nuevo índice XML selectivo con Transact-SQL**  
 Crear un índice XML selectivo llamado a la instrucción CREATE SELECTIVE XML INDEX. Para obtener más información, vea [CREAR ÍNDICE XML SELECTIVO &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se muestra la sintaxis para crear un índice XML selectivo. También se muestran varias variaciones de la sintaxis para describir las rutas de acceso que se van a indizar, con sugerencias opcionales de optimización.  
  
```sql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
  
##  <a name="alter"></a> Modificar un índice XML selectivo  
  
### <a name="how-to-alter-a-selective-xml-index"></a>Modificar un índice XML selectivo  
 **Modificar un índice XML selectivo con Transact-SQL**  
 Modificar un índice XML selectivo existente llamado a la instrucción ALTER INDEX. Para obtener más información, vea [ALTER INDEX &#40;Selective XML Indexes&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md).  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se muestra una instrucción ALTER INDEX. Esta instrucción agrega la ruta de acceso `'/a/b/m'` a la parte XQuery del índice y elimina la ruta de acceso `'/a/b/e'` de la parte SQL del índice creado en el ejemplo del tema [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md). La ruta de acceso que se va a eliminar se identifica por el nombre que se especificó cuando se creó.  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
  
##  <a name="drop"></a> Quitar un índice XML selectivo  
  
### <a name="how-to-drop-a-selective-xml-index"></a>Quitar un índice XML selectivo  
 **Quitar un índice XML selectivo con Transact-SQL**  
 Quitar un índice XML selectivo llamando a la instrucción DROP INDEX. Para obtener más información, vea [DROP INDEX &#40;índices XML selectivos&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Ejemplo**  
  
 En el ejemplo siguiente se muestra una instrucción DROP INDEX.  
  
```sql  
DROP INDEX sxi_index ON tbl  
```  
  
  
  
