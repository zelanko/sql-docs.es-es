---
title: Objetos que admite el asistente Generar scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 5
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f102fa4366106581c5f3ec4ff141d537531dbaa4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105334"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos que admite el asistente Generar scripts
  El asistente Generar y publicar scripts admite un subconjunto de los objetos admitidos por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos admitidos  
 La tabla siguiente enumera los objetos que se pueden publicar y que admite el Asistente para generar y publicar scripts.  
  
||||||  
|-|-|-|-|-|  
|Rol de aplicación|Rol de base de datos|esquema|Agregados definidos por el usuario|Vista<sup>1</sup>|  
|Ensamblado|Restricción DEFAULT|Procedimiento almacenado<sup>1</sup>|Tipos de datos definidos por el usuario|Colección de esquemas XML|  
|Restricción CHECK|Catálogo de texto completo|Synonym (Sinónimo)|Función definida por el usuario||  
|Procedimiento almacenado de CLR (common language runtime)<sup>1</sup>|Índice|Table|Tabla definida por el usuario||  
|Función CLR definida por el usuario|Regla|Usuario<sup>2</sup>|Tipo definido por el usuario||  
  
 <sup>1</sup> publicado sin cifrado.  
  
 <sup>2</sup> cualquier usuario no perteneciente al sistema que existen en la base de datos se publica como funciones.  
  
  