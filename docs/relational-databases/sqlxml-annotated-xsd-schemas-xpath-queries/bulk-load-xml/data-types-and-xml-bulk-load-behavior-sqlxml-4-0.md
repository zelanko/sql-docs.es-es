---
title: Tipos de datos y comportamiento de carga masiva XML (SQLXML)
description: Obtenga información sobre los tipos de datos y el comportamiento de carga masiva XML en SQLXML 4,0.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e77e4ca789a2abf5bb664221adb8911dd5a1bae5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529753"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de datos y comportamiento de la carga masiva XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Normalmente, se omiten los tipos de datos que se especifican en el esquema de asignación (XSD o tipo XDR y **SQL: DataType**), excepto en los casos siguientes:  
  
 En XSD:  
  
-   Si el tipo es **DateTime** u **Time**, debe especificar **SQL: DataType** porque la carga masiva XML realiza la conversión de datos antes de enviar los datos a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Cuando se realiza la carga masiva en una columna de tipo **uniqueidentifier** en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el valor XSD es un GUID que incluye llaves ({y}), debe especificar **SQL: DataType = "uniqueidentifier"** para quitar las llaves antes de que se inserte el valor en la columna. Si no se especifica **SQL: DataType** , el valor se envía con las llaves y se produce un error en la inserción.  
  
 Para obtener más información sobre **SQL: DataType**, vea [conversiones de tipos de datos y la anotación sql: datatype &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 En XDR:  
  
-   Si **DT: Type** es **DateTime**, **Time**, **DateTime.tz**o **Time.tz**, debe especificar los tipos de datos **DT: Type** y **SQL: DataType** , ya que la carga masiva XML realiza la conversión de datos antes de enviar los datos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Si los datos XML son del tipo **UUID**, se debe especificar **SQL: DataType** ; **DT: type = "UUID"** también es necesario, a menos que los datos sean datos de cadena. Si no especifica **DT: UUID**, la carga masiva XML acepta cadenas con llaves (y las quita si es necesario).  
  
-   Si los datos XML son **bin. base64** o **bin. hex**, debe especificar el tipo de datos XML con **DT: Type**. A continuación, la carga masiva XML carga los datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como una representación hexadecimal de los datos.  
  
  
