---
title: Generar un esquema XDR insertado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9641c727f52f9e108a368457a668aaf68e38f812
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716296"
---
# <a name="generate-an-inline-xdr-schema"></a>Generar un esquema XDR insertado
  La directiva **XMLDATA** de FOR XML devuelve un esquema XDR insertado junto con el resultado de la consulta. Sin embargo, el esquema XDR no admite todos los nuevos tipos de datos y otras mejoras incluidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. En su lugar, se puede solicitar un esquema XSD insertado mediante la [directiva XMLSCHEMA](generate-an-inline-xsd-schema.md).  
  
> [!IMPORTANT]  
>  La directiva XMLDATA para la opción FOR XML ha quedado desusada. Utilice la XSD generación en los modos RAW y AUTO. No hay sustitución para la directiva XMLDATA en modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Asimismo, es necesario tener en cuenta lo siguiente acerca de la compatibilidad del esquema XDR insertado:  
  
-   Si el resultado de la consulta FOR XML incluye columnas de tipo **xml** y se solicita un esquema XDR insertado, se devuelve un error. El esquema XDR insertado no admite estos tipos.  
  
-   Los tipos **(n)varchar(max)** y **(n)varbinary(max)** se asignarán a **(n)varchar(n)** y **varbinary(n)** respectivamente.  
  
-   Cuando el modo de compatibilidad se establece en 90 o más, los valores de **timestamp** se consideran datos **varbinary(8)** , se tratan como datos binarios y se devuelven en el resultado de la manera siguiente:  
  
    -   Cuando se especifica **binary base64** , se utiliza la codificación base 64.  
  
    -   Cuando no se especifica **binary base64** , se utiliza la codificación URL en modo AUTO.  
  
  
