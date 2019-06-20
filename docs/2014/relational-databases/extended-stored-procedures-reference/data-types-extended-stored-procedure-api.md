---
title: Tipos de datos (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 715cdc343e3a73781c06977fdb3d3d829d6bf533
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62511653"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipos de datos (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Para utilizar los tipos de datos de la API Procedimiento almacenado extendido, incluya el archivo de encabezado Srv.h en el programa.  
  
|Tipo de datos|Tipo de datos de SQL Server|Descripción|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|`binary`|Tipo de datos `binary`, longitud de 0 a 8.000 bytes.|  
|SRVBIGCHAR|`char`|Tipo de datos `character`, longitud de 0 a 8.000 bytes.|  
|SRVBIGVARBINARY|`varbinary`|Tipo de datos `binary` de longitud variable, longitud de 0 a 8.000 bytes.|  
|SRVBIGVARCHAR|`varchar`|Tipo de datos `character` de longitud variable, longitud de 0 a 8.000 bytes.|  
|SRVBINARY|`binary`|Tipo de datos `binary`.|  
|SRVBIT|`Bit`|Tipo de datos `bit`.|  
|SRVBITN|`bit null`|Tipo de datos `bit`, permite valores NULL.|  
|SRVCHAR|`char`|Tipo de datos `character`.|  
|SRVDATETIME|`datetime`|Tipo de datos `datetime` de 8 bytes.|  
|SRVDATETIM4|`smalldatetime`|4 bytes `smalldatetime` tipo de datos.|  
|SRVDATETIMN|**datetime null**|Tipo de datos `smalldatetime` o `datetime`, permite valores NULL.|  
|SRVDECIMAL|`decimal`|Tipo de datos `decimal`.|  
|SRVDECIMALN|`decimal null`|Tipo de datos `decimal`, permite valores NULL.|  
|SRVFLT4|`real`|4 bytes `real` tipo de datos.|  
|SRVFLT8|`float`|Tipo de datos `float` de 8 bytes.|  
|SRVFLTN|`real` &#124; `float null`|Tipo de datos `real` o `float`, permite valores NULL.|  
|SRVIMAGE|`image`|Tipo de datos `image`.|  
|SRVINT1|`tinyint`|1 byte `tinyint` tipo de datos.|  
|SRVINT2|`smallint`|2 bytes `smallint` tipo de datos.|  
|SRVINT4|`int`|4 bytes `int` tipo de datos.|  
|SRVINTN|`tinyint` &#124; `smallint` &#124; `int null`|Tipo de datos `tinyint`, `smallint` o `int`, permite valores NULL.|  
|SRVMONEY4|`smallmoney`|4 bytes `smallmoney` tipo de datos.|  
|SRVMONEY|`money`|Tipo de datos `money` de 8 bytes.|  
|SRVMONEYN|`money` &#124; `smallmoney null`|Tipo de datos `smallmoney` o `money`, permite valores NULL.|  
|SRVNCHAR|**nchar**|Tipo de datos `character` Unicode.|  
|SRVNTEXT|`ntext`|Tipo de datos `text` Unicode.|  
|SRVNUMERIC|`numeric`|Tipo de datos `numeric`.|  
|SRVNUMERICN|`numeric null`|Tipo de datos `numeric`, permite valores NULL.|  
|SRVNVARCHAR|**nvarchar**|Tipo de datos `character` Unicode de longitud variable.|  
|SRVTEXT|`text`|Tipo de datos `text`.|  
|SRVVARBINARY|`varbinary`|Tipo de datos `binary` de longitud variable.|  
|SRVVARCHAR|`varchar`|Tipo de datos `character` de longitud variable.|  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
