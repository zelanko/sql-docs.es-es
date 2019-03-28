---
title: Reglas de escape y caracteres no válidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aafacefa7a5bab5f8bc828f48384a79e17a13b11
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532157"
---
# <a name="invalid-characters-and-escape-rules"></a>Reglas de escape y caracteres no válidos
  En este tema se describe cómo la cláusula FOR XML controla los caracteres XML no válidos y se enumeran las reglas de escape para los caracteres que no son válidos en los nombres XML.  
  
## <a name="for-xml-and-invalid-characters"></a>FOR XML y los caracteres no válidos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea entidades de caracteres XML no válidos cuando estos caracteres se devuelven dentro de consultas FOR XML que no usan la directiva TYPE.  
  
 Aunque los analizadores compatibles con XML 1.0 generan errores de análisis, independientemente de que se hayan creado o no entidades con estos caracteres, el uso de estos caracteres con entidades se ajusta mejor a XML 1.1. El uso de estos caracteres con entidades también se ajusta mejor a las futuras versiones del estándar XML. Además, simplifica la depuración, porque el punto de código del carácter no válido pasa a ser visible.  
  
 Los usuarios de herramientas XML no necesitan ninguna solución porque el analizador XML generará errores de todos modos en el punto del flujo de datos donde haya caracteres no válidos. Si se utilizan herramientas no XML, este cambio puede exigir la actualización de la lógica de programación para poder buscar estos caracteres como valores con entidades.  
  
 En los siguientes caracteres de espacio en blanco, ha cambiado la forma de crear entidades en consultas FOR XML con objeto de conservar su presencia a lo largo de los recorridos de ida y vuelta:  
  
-   En contenido de elemento y atributos: **hex(0D)** (retorno de carro)  
  
-   En contenido de atributo: **hex(09)** (tabulador), **hex(0A)** (avance de línea)  
  
 Estos caracteres se conservan en la salida y no se normalizarán con ningún analizador.  
  
## <a name="escape-rules"></a>Reglas de escape  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contienen caracteres que no son válidos en los nombres XML, como los espacios, se traducen a nombres XML, de forma que los caracteres no válidos se convierten en codificaciones de entidad numérica de escape.  
  
 Solo hay dos caracteres no alfabéticos que pueden incluirse en un nombre XML: los dos puntos (:) y el carácter de subrayado (_). Dado que el carácter de dos puntos está reservado para los espacios de nombres, se elige el subrayado como carácter de escape. A continuación se muestran las reglas de escape que se utilizan en la codificación:  
  
-   Cualquier carácter UCS-2 que no sea válido como carácter de nombre XML, conforme a la especificación XML 1.0, se convierte en un carácter de escape con formato _xHHHH\_. HHHH hace referencia al código UCS-2 hexadecimal de cuatro dígitos correspondiente al carácter que ocupa el primer lugar en función del bit más significativo. Por ejemplo, el nombre de tabla **Order Details** se codifica como Order_x0020_Details.  
  
-   Los caracteres que no se ajustan al dominio UCS-2 (como las adiciones UCS-4 del rango de U+00010000 a U+0010FFFF) se codifican como _xHHHHHHHH\_. HHHHHHHH hace referencia al código UCS-4 hexadecimal de ocho dígitos correspondiente al carácter, para el modo de compatibilidad con versiones anteriores de SQL Server 2000. De lo contrario, los caracteres se codifican como _xHHHHHH\_, para ajustarse a la norma ISO.  
  
-   No es necesario convertir en carácter de escape el carácter de subrayado, a menos que vaya seguido del carácter x. Por ejemplo, no es necesario codificar el nombre de tabla **Order_Details** .  
  
-   Los dos puntos de los identificadores no se convierten en un carácter de escape, por lo que la consulta FOR XML puede generar nombres de elementos y atributos de espacio de nombres. Por ejemplo, la siguiente consulta genera un atributo de espacio de nombres con un carácter de dos puntos en el nombre:  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     La consulta genera este resultado:  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     Tenga en cuenta que el uso de WITH XMLNAMESPACES es la forma recomendada de agregar espacios de nombres XML.  
  
## <a name="see-also"></a>Vea también  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
