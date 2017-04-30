---
title: Recuperar y consultar datos XML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cff6370e1e57b4f1163100f029bd56d7bf63e552
ms.lasthandoff: 04/11/2017

---
# <a name="retrieve-and-query-xml-data"></a>Recuperar y consultar datos XML
  En este tema se describen las opciones de consulta que se tienen que especificar para consultar datos XML. También describe las partes de las instancias XML que no se conservan cuando se almacenan en bases de datos.  
  
##  <a name="features"></a> Características de una instancia de XML que no se mantienen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva el contenido de la instancia XML, pero no conserva los aspectos de la instancia XML que no se consideran significativos en el modelo de datos XML. Esto significa que una instancia XML recuperada no podría ser idéntica a la instancia que se almacenó en el servidor pero contendrá la misma información.  
  
### <a name="xml-declaration"></a>Declaración XML  
 La declaración XML de una instancia no se conserva cuando la instancia está almacenada en la base de datos. Por ejemplo:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 El resultado es `<doc/>`.  
  
 No se conserva la declaración XML, como `<?xml version='1.0'?>`, al almacenar los datos XML en una instancia de tipo de datos **xml** . es así por diseño. La declaración XML () y sus atributos (versión/codificación/independiente) se pierden cuando los datos se convierten al tipo **xml**. La declaración XML se trata como una directiva del analizador XML. Los datos XML se almacenan internamente como ucs-2. Se conservan todos los demás PI en la instancia XML.  
  
  
### <a name="order-of-attributes"></a>Orden de atributos  
 El orden de los atributos de una instancia XML no se conserva. Al consultar la instancia XML almacenada en la columna de tipo **xml** , el orden de los atributos del XML resultante puede diferir con respecto a la instancia XML original.  
  
  
### <a name="quotation-marks-around-attribute-values"></a>Comillas alrededor de valores de atributo  
 Alrededor de los valores de atributo no se conservan las comillas simples ni las comillas dobles. Los valores de atributo se almacenan en la base de datos como un par de nombre y valor. Las comillas no se almacenan. Cuando se ejecuta una consulta XQuery en una instancia XML, el XML resultante se serializa con comillas dobles alrededor de los valores de atributo.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 Las dos consultas devuelven = `<root a="1" />`.  
  
  
### <a name="namespace-prefixes"></a>Prefijos de espacio de nombres  
 No se conservan los prefijos de espacios de nombres. Cuando se especifica XQuery en una columna de tipo **xml** , el resultado XML serializado puede devolver distintos prefijos de espacios de nombres.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 El prefijo de espacio de nombres del resultado puede ser distinto. Por ejemplo:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="query"></a> Establecer opciones de consulta necesarias  
 Cuando se consultan variables o columnas de tipo **xml** mediante métodos del tipo de datos **xml** , se deben establecer las siguientes opciones como se indica.  
  
|Opciones de SET|Valores requeridos|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 Si no se establecen las opciones como se indica, no funcionarán las consultas y modificaciones de los métodos del tipo de datos **xml** .  
  
  
## <a name="see-also"></a>Vea también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
