---
title: Comando de TAG DELETE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eabecbc399751f03e9e5c25b32423ce0839072dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198252"
---
# <a name="delete-tag-command"></a>Eliminar etiqueta, comando
Quita una etiqueta o etiquetas de un archivo de índice compuesto (.cdx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]]...  
 Especifica una etiqueta para quitar de un archivo de índice compuesto. Puede eliminar varias etiquetas con una etiqueta eliminar mediante la inclusión de una lista de nombres de etiqueta separados por comas. Si existen dos o más etiquetas con el mismo nombre en los archivos de índice abierto, puede quitar una etiqueta de un archivo de índice específica mediante la inclusión de *CDXFileName*.  
  
 Todos los [OF *CDXFileName*]  
 Quita todas las etiquetas de un archivo de índice compuesto. Si la tabla actual tiene un archivo de índice compuesto estructural, se quitan todas las etiquetas desde el archivo de índice, se elimina el archivo de índice desde el disco y se quita la marca de encabezado de la tabla que indica la presencia de un archivo de índice compuesto estructural. Use todo ello con OF *CDXFileName* para quitar todas las etiquetas de un archivo abierto índice compuesto distinto del archivo de índice compuesto estructural.  
  
## <a name="remarks"></a>Comentarios  
 Archivos de índice compuesto, creados con el índice, contienen las etiquetas correspondientes a las entradas de índice. Eliminar etiqueta a la que se usa para quitar una etiqueta o etiquetas de los archivos de índice compuesto abierto. Puede eliminar sólo las etiquetas de los archivos de índice compuesto abiertos en el área de trabajo actual. Si quita todas las etiquetas de un archivo de índice compuesto, se elimina el archivo desde el disco.  
  
 Visual FoxPro busca primero una etiqueta en el archivo de índice compuesto estructural (si está abierto). Si la etiqueta no se encuentra en el archivo de índice compuesto estructural, Visual FoxPro, busca la etiqueta en los demás archivos de índice compuesto abierto.  
  
## <a name="see-also"></a>Vea también  
 [Comando de índice](../../odbc/microsoft/index-command.md)
