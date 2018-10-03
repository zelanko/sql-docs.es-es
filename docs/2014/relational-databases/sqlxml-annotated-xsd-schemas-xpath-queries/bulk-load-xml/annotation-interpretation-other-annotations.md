---
title: Otras anotaciones (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe23d1fbcae65bf77c66ffa423d597cb1539a1eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115770"
---
# <a name="other-annotations-sqlxml-40"></a>Otras anotaciones (SQLXML 4.0)
  Además de las anotaciones descritas en los temas anteriores de esta sección, la carga masiva de XML interpreta estas otras anotaciones del modo siguiente:  
  
 `sql:id-prefix`  
 Si el esquema especifica prefijos para los datos XML, la carga masiva de XML quita los prefijos antes de enviar los datos a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:use-cdata`  
 La carga masiva de XML lee el texto que está almacenado en las secciones CDATA y lo envía a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:url-encode`  
 La carga masiva de XML no admite esta anotación. Por ejemplo, no puede especificar una dirección URL en la entrada de datos XML y esperar que la carga masiva de XML lea los datos de esa ubicación para almacenarlos en la base de datos.  
  
 `sql:is-mapping-schema`  
 La carga masiva de XML no admite esta anotación, ni tampoco admite `sql:id`.  
  
> [!NOTE]  
>  La carga masiva de XML no admite los esquemas de asignación insertados.  
  
 `sql:key-fields`  
 La carga masiva de XML omite siempre esta anotación.  
  
## <a name="see-also"></a>Vea también  
 [Interpretación de anotaciones &#40;SQLXML 4.0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
