---
title: Recuperar y consultar datos XML | Microsoft Docs
description: Obtenga información sobre las opciones de consulta que se deben especificar al consultar datos XML y sobre las partes de las instancias XML que no se conservan cuando se almacenan en bases de datos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86f908d6aa221b2c69be3d8960efac929cbf5306
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738400"
---
# <a name="retrieve-and-query-xml-data"></a>Recuperar y consultar datos XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  En este tema se describen las opciones de consulta que se tienen que especificar para consultar datos XML. También describe las partes de las instancias XML que no se conservan cuando se almacenan en bases de datos.  
  
##  <a name="features-of-an-xml-instance-that-are-not-preserved"></a><a name="features"></a> Características de una instancia de XML que no se mantienen  
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
  
  
##  <a name="setting-required-query-options"></a><a name="query"></a> Establecer opciones de consulta necesarias  
 Cuando se consultan variables o columnas de tipo **xml** mediante métodos del tipo de datos **xml** , se deben establecer las siguientes opciones como se indica.  
  
|Opciones de SET|Valores requeridos|  
|-----------------|---------------------|  
|ANSI_NULLS|ACTIVAR|  
|ANSI_PADDING|ACTIVAR|  
|ANSI_WARNINGS|ACTIVAR|  
|ARITHABORT|ACTIVAR|  
|CONCAT_NULL_YIELDS_NULL|ACTIVAR|  
|NUMERIC_ROUNDABORT|Apagado|  
|QUOTED_IDENTIFIER|ACTIVAR|  
  
 Si no se establecen las opciones como se indica, no funcionarán las consultas y modificaciones de los métodos del tipo de datos **xml** .  
  
  
## <a name="see-also"></a>Consulte también  
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
