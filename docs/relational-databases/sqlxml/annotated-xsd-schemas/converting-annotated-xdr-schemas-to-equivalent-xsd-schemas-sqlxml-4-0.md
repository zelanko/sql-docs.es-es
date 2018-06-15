---
title: Convertir esquemas XDR anotados en esquemas XSD equivalentes (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a841cf9e5bcfe3c1de5c199fa29984c709631598
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32969830"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>Convertir esquemas XDR anotados en esquemas XSD equivalentes (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El lenguaje de definición de esquemas XML (XSD) es el sucesor del lenguaje de definición de esquemas reducidos de datos XML (XDR). Con la introducción de la compatibilidad con XSD en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, se asume que los nuevos esquemas anotados se crean utilizando XSD. SQLXML 4.0 incluye una herramienta de conversión de XDR a XSD diseñada para ayudarle a convertir sus esquemas XDR anotados en esquemas XSD equivalentes.  
  
> [!IMPORTANT]  
>  Utilice esta herramienta únicamente cuando desee convertir los esquemas XDR anotados en XSD para utilizarlos con SQLXML 4.0. No se trata de una herramienta de conversión de XDR a XSD de uso general. Es posible que los esquemas XSD convertidos no se comporten de mismo modo que los esquemas XDR originales cuando se utilicen en otros entornos.  
  
 Si el archivo XDR de entrada especifica la codificación dentro de la declaración XML, ésta se convierte en la codificación del archivo XSD de salida generado.  
  
 La herramienta de conversión (Cvtschema.exe) se instala en la carpeta Archivos de programa\SQLXML 4.0\bin y se ejecuta en el símbolo del sistema.  
  
 Ésta es la sintaxis general:  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 Donde:  
  
 XDRFileName  
 Es el nombre del archivo XDR que se convertirá en XSD. La herramienta lee el archivo XDR de entrada y crea un archivo XSD de salida en el directorio de trabajo actual. Si el archivo de entrada tiene la extensión .xdr o .xml, el archivo XSD de salida se crea con el mismo nombre pero con la extensión .xsd. Si la extensión de nombre de archivo de entrada es distinto de .xml o .xdr (o si la extensión está presente), se crea el archivo de salida con el mismo nombre y la extensión .xsd se anexa al nombre de archivo de entrada. Por ejemplo, si el nombre del archivo XDR de entrada es SampleFile.abc, el XSD resultante se guardará como SampleFile.abc.xsd.  
  
 -y  
 (Opcional) Sobrescribe el archivo XSD existente con el archivo XSD generado por la herramienta de conversión. Si no se especifica la marca, la herramienta le solicita que especifique si desea sobrescribir el archivo XSD existente y le ofrece la posibilidad de cambiar el nombre del archivo de salida.  
  
 -w  
 (Opcional) Devuelve advertencias de errores recuperables que se generan durante el proceso de conversión de la herramienta. De forma predeterminada, la herramienta solo muestra los mensajes de errores irrecuperables.  
  
 -?  
 Devuelve una lista de opciones que puede especificar con **cvtschema**, junto con una explicación.  
  
## <a name="see-also"></a>Vea también  
 [Asignar tipos de datos XSD a tipos de datos de XPath &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [Las anotaciones XSD &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
