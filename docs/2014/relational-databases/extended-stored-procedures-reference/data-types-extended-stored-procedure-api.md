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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62511653"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipos de datos (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Para utilizar los tipos de datos de la API Procedimiento almacenado extendido, incluya el archivo de encabezado Srv.h en el programa.  
  
|Tipo de datos|Tipos de datos de SQL Server|Descripción|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|`binary`|Tipo de datos `binary`, longitud de 0 a 8.000 bytes.|  
|SRVBIGCHAR|`char`|Tipo de datos `character`, longitud de 0 a 8.000 bytes.|  
|SRVBIGVARBINARY|`varbinary`|Tipo de datos `binary` de longitud variable, longitud de 0 a 8.000 bytes.|  
|SRVBIGVARCHAR|`varchar`|Tipo de datos `character` de longitud variable, longitud de 0 a 8.000 bytes.|  
|SRVBINARY|`binary`|`binary`tipo de datos.|  
|SRVBIT|`Bit`|`bit`tipo de datos.|  
|SRVBITN|`bit null`|Tipo de datos `bit`, permite valores NULL.|  
|SRVCHAR|`char`|`character`tipo de datos.|  
|SRVDATETIME|`datetime`|Tipo de datos `datetime` de 8 bytes.|  
|SRVDATETIM4|`smalldatetime`|tipo de datos `smalldatetime` de 4 bytes.|  
|SRVDATETIMN|**DateTime null**|Tipo de datos `smalldatetime` o `datetime`, permite valores NULL.|  
|SRVDECIMAL|`decimal`|`decimal`tipo de datos.|  
|SRVDECIMALN|`decimal null`|Tipo de datos `decimal`, permite valores NULL.|  
|SRVFLT4|`real`|tipo de datos `real` de 4 bytes.|  
|SRVFLT8|`float`|Tipo de datos `float` de 8 bytes.|  
|SRVFLTN|`real`&#124;`float null`|Tipo de datos `real` o `float`, permite valores NULL.|  
|SRVIMAGE|`image`|`image`tipo de datos.|  
|SRVINT1|`tinyint`|tipo de datos `tinyint` de 1 byte.|  
|SRVINT2|`smallint`|tipo de datos `smallint` de 2 bytes.|  
|SRVINT4|`int`|tipo de datos `int` de 4 bytes.|  
|SRVINTN|`tinyint`&#124; `smallint` &#124;`int null`|Tipo de datos `tinyint`, `smallint` o `int`, permite valores NULL.|  
|SRVMONEY4|`smallmoney`|tipo de datos `smallmoney` de 4 bytes.|  
|SRVMONEY|`money`|Tipo de datos `money` de 8 bytes.|  
|SRVMONEYN|`money`&#124;`smallmoney null`|Tipo de datos `smallmoney` o `money`, permite valores NULL.|  
|SRVNCHAR|**nchar**|Tipo de datos `character` Unicode.|  
|SRVNTEXT|`ntext`|Tipo de datos `text` Unicode.|  
|SRVNUMERIC|`numeric`|`numeric`tipo de datos.|  
|SRVNUMERICN|`numeric null`|Tipo de datos `numeric`, permite valores NULL.|  
|SRVNVARCHAR|**nvarchar**|Tipo de datos `character` Unicode de longitud variable.|  
|SRVTEXT|`text`|`text`tipo de datos.|  
|SRVVARBINARY|`varbinary`|Tipo de datos `binary` de longitud variable.|  
|SRVVARCHAR|`varchar`|Tipo de datos `character` de longitud variable.|  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
