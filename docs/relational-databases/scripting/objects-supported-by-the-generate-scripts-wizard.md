---
title: Objetos que admite el asistente Generar scripts | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fddad739f540eaff93834cc7a4f0f6efbcbd500
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos que admite el asistente Generar scripts
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] El asistente Generar y publicar scripts admite un subconjunto de los objetos que admite [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Objetos admitidos  
 La tabla siguiente enumera los objetos que se pueden publicar y que admite el Asistente para generar y publicar scripts.  
  
||||||  
|-|-|-|-|-|  
|Rol de aplicación|Rol de base de datos|esquema|Agregados definidos por el usuario|Ver*|  
|Ensamblado|Restricción DEFAULT|Procedimiento almacenado*|Tipos de datos definidos por el usuario|Colección de esquemas XML|  
|Restricción CHECK|Catálogo de texto completo|Synonym (Sinónimo)|Función definida por el usuario||  
|Procedimiento almacenado de CLR (Common Language Runtime)*|Índice|Table|Tabla definida por el usuario||  
|Función CLR definida por el usuario|Regla|Usuario**|Tipo definido por el usuario||  
  
 *Publicado sin cifrado.  
  
 **Cualquier usuario no perteneciente al sistema que exista en la base de datos se publica como Funciones.  
  
  
