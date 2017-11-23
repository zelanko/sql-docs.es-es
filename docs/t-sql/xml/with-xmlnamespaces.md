---
title: WITH XMLNAMESPACES (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs: TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: db002fd372fd69972b4f150c14c95342686f85f3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Declara uno o varios espacios de nombres XML.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *xml_namespace_uri*  
 Identificador uniforme de recursos (URI) que identifica el espacio de nombres XML que se va a declarar. *xml_namespace_uri* es una cadena SQL.  
  
 *xml_namespace_prefix*  
 Especifica un prefijo que se van a asignar y asociado con el valor de identificador URI de espacio de nombres especificado en *xml_namespace_uri*. *xml_namespace_prefix* debe ser un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador.  
  
## <a name="remarks"></a>Comentarios  
 Al utilizar la cláusula WITH XMLNAMESPACES en una instrucción que también incluye una expresión de tabla común, la cláusula WITH XMLNAMESPACES debe preceder a la expresión de tabla común en la instrucción.  
  
 Estas son las reglas generales de sintaxis que se aplican cuando se usa la cláusula WITH XMLNAMESPACES:  
  
-   Cada declaración de espacio de nombres XML debe contener al menos un elemento de declaración de espacio de nombres XML predeterminado.  
  
-   Cada prefijo de espacio de nombres XML utilizado debe ser un nombre no colonizado (NCName) y que el carácter de dos puntos (:) no forme parte del nombre.  
  
-   No se puede definir un prefijo de espacio de nombres dos veces.  
  
-   Los prefijos del espacio de nombres XML y los URI distinguen entre mayúsculas y minúsculas.  
  
-   No se puede declarar el prefijo del espacio de nombres XML `xmlns` .  
  
-   No se puede reemplazar el prefijo del espacio de nombres `xml` con un espacio de nombres distinto del URI de los espacios de nombres `'http://www.w3.org/XML/1998/namespace'` y este URI no se puede asignar a diferentes prefijos.  
  
-   No se puede volver a declarar el prefijo del espacio de nombres XML `xsi` cuando se va a utilizar la directiva ELEMENTS XSINIL en la consulta.  
  
-   Los valores de la cadena del URI se codifican según la página de códigos de la intercalación de la base de datos actual y se traducen internamente a Unicode.  
  
-   El espacio de nombres XML URI será un espacio en blanco siguiendo el espacio en blanco XSD contraer las reglas que se usan para **xs: anyURI**. Además, tenga en cuenta que no se definirán entidades ni se eliminarán entidades en los valores de URI del espacio de nombres XML.  
  
-   Se comprobará el URI del espacio de nombres XML para buscar caracteres XML 1.0 no válidos y se generará un error si se encuentran (por ejemplo, U+0007).  
  
-   El URI del espacio de nombres XML (después de eliminar los espacios en blanco) no puede ser una cadena de longitud cero o se producirá un error de URI de espacio de nombres vacío no válido.  
  
-   La palabra clave XMLNAMESPACES está reservada en el contexto de la cláusula WITH.  
  
## <a name="examples"></a>Ejemplos  
 Para obtener ejemplos, vea [agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
