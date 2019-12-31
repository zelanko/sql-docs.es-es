---
title: Objetos que admite el asistente Generar scripts
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c266cf82a6f790d20cec3b3ec94f3c5e42b74b5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241991"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos que admite el asistente Generar scripts
  El asistente Generar y publicar scripts admite un subconjunto de los objetos admitidos por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos admitidos  
 La tabla siguiente enumera los objetos que se pueden publicar y que admite el Asistente para generar y publicar scripts.  
  
||||||  
|-|-|-|-|-|  
|Rol de aplicación|Rol de base de datos|Schema|Agregados definidos por el usuario|Vista<sup>1</sup>|  
|Ensamblado|Restricción DEFAULT|Procedimiento almacenado<sup>1</sup>|Tipos de datos definidos por el usuario|Colección de esquemas XML|  
|Restricción CHECK|Catálogo de texto completo|Synonym (Sinónimo)|Función definida por el usuario||  
|Procedimiento almacenado de CLR (Common Language Runtime)<sup>1</sup>|Índice|Tabla|Tabla definida por el usuario||  
|Función CLR definida por el usuario|Regla|Usuario<sup>2</sup>|Tipo definido por el usuario||  
  
 <sup>1</sup> publicado sin cifrado.  
  
 <sup>2</sup> cualquier usuario que no sea del sistema que exista en la base de datos se publicará como rol.  
  
  
