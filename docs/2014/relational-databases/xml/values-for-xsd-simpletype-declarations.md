---
title: Valores para declaraciones &lt;xsd:simpleType&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6682bdb7443ae9ee41bd1a7f77d7b5d5ae4d7359
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702303"
---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>Values for &lt;xsd:simpleType&gt; Declarations (Valores para declaraciones &lt;xsd:simpleType&gt;)
  En la tabla siguiente se presentan las restricciones que se aplican, en función de todas las enumeraciones de tipo simple XSD reconocidas.  
  
 Además, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite el uso del valor NaN en declaraciones **\<xsd:simpleType>** . El servidor rechaza los esquemas que incluyen valores NaN.  
  
|Tipo simple|Limitación|  
|-----------------|----------------|  
|`duration`|La parte del año tiene que estar dentro del intervalo de-2 <sup>^</sup> 31 a 2 <sup>^</sup> 31-1. El mes, día, hora, minuto y segundo deben estar todos dentro del intervalo de 0 a 9999. La segunda parte tiene tres dígitos adicionales de precisión a la derecha del separador decimal.|  
|`dateTime`|La parte de la hora del subcampo de la zona horaria debe estar dentro del intervalo aceptado de -14 a +14. La parte del año se debe encontrar en el intervalo de 1 a 9999. La parte del mes se debe encontrar en el intervalo de 1 a 12. La parte del día se debe encontrar en el intervalo de 1 a 31 y debe ser una fecha válida del calendario. Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta y devuelve un error en el caso de una fecha no válida, como 1974-02-31, porque el mes de febrero no tiene 31 días.<br /><br /> El segundo componente admite precisión de 100 nanosegundos. La indicación de zona horaria es opcional.<br /><br /> SQL Server 2005 admitía años en el intervalo de -9999 a 9999. Ahora, SQL Server admite un intervalo más restringido de años. Para obtener más información, vea [comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md).|  
|`date`|La parte del año se debe encontrar en el intervalo de 1 a 9999. La parte del mes se debe encontrar en el intervalo de 1 a 12. La parte del día se debe encontrar en el intervalo de 1 a 31 y debe ser una fecha válida del calendario. Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta y devuelve un error en el caso de una fecha no válida, como 1974-02-31, porque el mes de febrero no tiene 31 días.<br /><br /> SQL Server 2005 admitía años en el intervalo de -9999 a 9999. Ahora, SQL Server admite un intervalo más restringido de años. Para obtener más información, vea [comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md).|  
|`gYearMonth`|La parte del año se debe encontrar en el intervalo de -9999 a 9999.|  
|`gYear`|La parte del año se debe encontrar en el intervalo de -9999 a 9999.|  
|`gMonthDay`|La parte del mes se debe encontrar en el intervalo de 1 a 12. La parte del día se debe encontrar en el intervalo de 1 a 31.|  
|`gDay`|La parte del día se debe encontrar en el intervalo de 1 a 31.|  
|`gMonth`|La parte del mes se debe encontrar en el intervalo de 1 a 12.|  
|`decimal`|Los valores de este tipo deben cumplir el formato de tipo numérico de SQL. Este tipo representa internamente la compatibilidad con los números de hasta 38 dígitos, diez de los cuales están reservados para la precisión en fracciones.|  
|`float`|Los valores de este tipo deben cumplir el formato del tipo `real` de SQL.|  
|**double**|Los valores de este tipo deben cumplir el formato del tipo `float` de SQL.|  
|`string`|Los valores de este tipo deben cumplir el formato del tipo `nvarchar(max)` de SQL.|  
|`anyURI`|Los valores de este tipo no pueden superar los 4.000 caracteres Unicode de longitud.|  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
