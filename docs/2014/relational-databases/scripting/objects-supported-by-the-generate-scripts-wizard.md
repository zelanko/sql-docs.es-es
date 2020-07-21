---
title: Objetos que admite el asistente Generar scripts
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ddc1da0d2f87fc12dfbe034a683802f54b7d34f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85009747"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos que admite el asistente Generar scripts
  El asistente Generar y publicar scripts admite un subconjunto de los objetos admitidos por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos admitidos  
 La tabla siguiente enumera los objetos que se pueden publicar y que admite el Asistente para generar y publicar scripts.  
  
||||||  
|-|-|-|-|-|  
|Rol de aplicación|Rol de base de datos|Schema|Agregados definidos por el usuario|Vista<sup>1</sup>|  
|Assembly|Restricción DEFAULT|Procedimiento almacenado<sup>1</sup>|Tipos de datos definidos por el usuario|Colección de esquemas XML|  
|Restricción CHECK|Catálogo de texto completo|Synonym (Sinónimo)|Función definida por el usuario||  
|Procedimiento almacenado de CLR (Common Language Runtime)<sup>1</sup>|Índice|Tabla|Tabla definida por el usuario||  
|Función CLR definida por el usuario|Regla|Usuario<sup>2</sup>|Tipo definido por el usuario||  
  
 <sup>1</sup> publicado sin cifrado.  
  
 <sup>2</sup> cualquier usuario que no sea del sistema que exista en la base de datos se publicará como rol.  
  
  
