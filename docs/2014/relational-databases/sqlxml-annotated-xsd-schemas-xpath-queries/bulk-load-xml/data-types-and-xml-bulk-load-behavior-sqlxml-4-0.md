---
title: Tipos de datos y XML (SQLXML 4.0) del comportamiento de carga de forma masiva | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2eb9af2b353760f5b195b95d6a9f9d5d1efc9b
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013416"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de datos y comportamiento de la carga masiva XML (SQLXML 4.0)
  Generalmente se omiten los tipos de datos que se especifican en el esquema de asignación (XSD o tipo XDR y `sql:datatype`), excepto en los casos siguientes:  
  
 En XSD:  
  
-   Si el tipo es `dateTime` o `time`, debe especificar `sql:datatype` porque la carga masiva XML realiza la conversión de datos antes de enviarlos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Cuando se carga masiva en una columna de `uniqueidentifier` escriba [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el valor XSD es un GUID que incluye llaves ({y}), se debe especificar **SQL: DataType = "uniqueidentifier"** para quitar las llaves antes de que el valor es Insertar en la columna. Si no se especifica `sql:datatype`, el valor se envía con las llaves y se produce un error en la inserción.  
  
 Para obtener más información acerca de `sql:datatype`, consulte [conversiones de tipos de datos y la anotación SQL: DataType &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 En XDR:  
  
-   Si `dt:type` es `datetime`, `time`, `dateTime.tz` o `time.tz`, debe especificar los tipos de datos `dt:type` y `sql:datatype` porque la carga masiva XML realiza la conversión de datos antes de enviar los datos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Si los datos XML están de tipo `uuid`, `sql:datatype` debe especificarse; **dt: Type = "uuid"** también es necesario, a menos que los datos son datos de cadena. Si no especifica `dt:uuid`, la carga masiva XML acepta cadenas con llaves (y las quita si es necesario).  
  
-   Si los datos XML son `bin.base64` o `bin.hex`, debe especificar el tipo de datos XML con `dt:type`. A continuación, la carga masiva XML carga los datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como una representación hexadecimal de los datos.  
  
  
