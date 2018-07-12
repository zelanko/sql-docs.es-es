---
title: Compatibilidad de FOR XML con el tipo de datos de marca de tiempo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type
ms.assetid: 4e1920e1-e7a4-4069-965e-3f6039a6099e
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2411dca6acb605e5a543f8bc89982b6783f9f70a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240145"
---
# <a name="for-xml-support-for-the-timestamp-data-type"></a>Compatibilidad de FOR XML con el tipo de datos de marca de tiempo
  En la transformación FOR XML, los valores de tipo **timestamp** se tratan como datos **varbinary(8)** y siempre se codifican en base 64. El esquema XSD o XDR, si se solicita, refleja este tipo.  
  
```  
drop table t  
go  
create table t  
(c1 int,  
 c2 timestamp)  
go  
  
insert t values(1, null)  
go  
select * from t  
for xml auto, xmldata  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<Schema name="Schema1"   
        xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="t" content="empty" model="closed">  
    <AttributeType name="c1" dt:type="i4" />  
    <AttributeType name="c2" dt:type="bin.base64" />  
    <attribute type="c1" />  
    <attribute type="c2" />  
  </ElementType>  
</Schema>  
<t xmlns="x-schema:#Schema1" c1="1" c2="AAAAAAAAH04=" />  
```  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
