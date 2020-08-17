---
description: Eliminar etiqueta, comando
title: Comando eliminar etiqueta | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16eeedd8d9995cf636791688179ba21002411aea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340891"
---
# <a name="delete-tag-command"></a>Eliminar etiqueta, comando
Quita una etiqueta o etiquetas de un archivo de índice compuesto (. CDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TagName1* OF *CDXFileName1*[, *TagName2*[of *CDXFileName2*]]...  
 Especifica la etiqueta que se va a quitar de un archivo de índice compuesto. Puede eliminar varias etiquetas con una etiqueta de eliminación si incluye una lista de nombres de etiquetas separadas por comas. Si hay dos o más etiquetas con el mismo nombre en los archivos de índice abierto, puede quitar una etiqueta de un archivo de índice específico incluyendo *CDXFileName*.  
  
 TODOS [de *CDXFileName*]  
 Quita todas las etiquetas de un archivo de índice compuesto. Si la tabla actual tiene un archivo de índice compuesto estructural, todas las etiquetas se quitan del archivo de índice, el archivo de índice se elimina del disco y se quita la marca del encabezado de la tabla que indica la presencia de un archivo de índice compuesto estructural asociado. Use ALL con *CDXFileName* para quitar todas las etiquetas de un archivo de índice compuesto abierto que no sea el archivo de índice compuesto estructural.  
  
## <a name="remarks"></a>Observaciones  
 Los archivos de índice compuesto, creados con el índice, contienen etiquetas correspondientes a las entradas de índice. Eliminar etiqueta se usa para quitar una etiqueta o etiquetas de los archivos de índice compuesto abiertos. Solo se pueden eliminar las etiquetas de los archivos de índice compuesto abiertos en el área de trabajo actual. Si quita todas las etiquetas de un archivo de índice compuesto, el archivo se elimina del disco.  
  
 Visual FoxPro busca primero una etiqueta en el archivo de índice compuesto estructural (si está abierto). Si la etiqueta no está en el archivo de índice compuesto estructural, Visual FoxPro busca la etiqueta en los otros archivos de índice compuesto abierto.  
  
## <a name="see-also"></a>Consulte también  
 [Comando de índice](../../odbc/microsoft/index-command.md)
