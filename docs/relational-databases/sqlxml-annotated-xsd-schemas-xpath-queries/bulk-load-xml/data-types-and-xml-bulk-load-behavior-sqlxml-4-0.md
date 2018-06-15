---
title: Tipos de datos y XML de forma masiva el comportamiento de carga (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eb6f8a64d48e6fa1336a4f56ca63b07873ee7168
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32967437"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de datos y comportamiento de la carga masiva XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Los tipos de datos que se especifican en el esquema de asignación (tipo XSD o XDR y **SQL: DataType**) generalmente se ignoran, excepto en los casos siguientes:  
  
 En XSD:  
  
-   Si el tipo es **dateTime** o **tiempo**, debe especificar el **SQL: DataType** porque la carga masiva XML realiza la conversión de datos antes de enviar los datos a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Cuando la carga masiva en una columna de **uniqueidentifier** escriba [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el valor XSD es un GUID que incluye llaves ({y}), se debe especificar **SQL: DataType = "uniqueidentifier"** a Quite las llaves antes de que el valor se inserta en la columna. Si **SQL: DataType** no se especifica, el valor se envía con las llaves y se produce un error en la inserción.  
  
 Para obtener más información acerca de **SQL: DataType**, consulte [conversiones de tipos de datos y la anotación SQL: DataType &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 En XDR:  
  
-   Si el **dt: Type** es **datetime**, **tiempo**, **dateTime.tz**, o **time.tz**, debe especificar tanto el **dt: Type** y **SQL: DataType** tipos de datos porque la carga masiva XML realiza la conversión de datos antes de enviar los datos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Si los datos XML están de tipo **uuid**, **SQL: DataType** debe especificarse; **dt: Type = "uuid"** también es necesario, a menos que los datos son datos de cadena. Si no se especifica **dt:uuid**, carga masiva XML acepta cadenas con llaves (y los elimina si es necesario).  
  
-   Si los datos XML son **bin.base64** o **bin.hex**, debe especificar el tipo de datos XML con **dt: Type**. A continuación, la carga masiva XML carga los datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como una representación hexadecimal de los datos.  
  
  
