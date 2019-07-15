---
title: Objetos que admite el asistente Generar scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 181afad8fbb3961a61b307a1ac74e8a750003f20
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690199"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Objetos que admite el asistente Generar scripts
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  El asistente Generar y publicar scripts admite un subconjunto de los objetos admitidos por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
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
  
  
