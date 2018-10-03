---
title: Objetos que admite el asistente Generar scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32148fabf2e10e620f308bad63648e3e74f48e86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202465"
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
|Procedimiento almacenado CLR (common language runtime)<sup>1</sup>|Índice|Table|Tabla definida por el usuario||  
|Función CLR definida por el usuario|Regla|Usuario<sup>2</sup>|Tipo definido por el usuario||  
  
 <sup>1</sup> publicado sin cifrado.  
  
 <sup>2</sup> los usuarios que no son de sistema que existen en la base de datos se publican como rol.  
  
  
