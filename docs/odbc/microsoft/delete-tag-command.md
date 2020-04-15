---
title: COMANDO DELETE TAG (ELIMINAR comando de TAG) Microsoft Docs
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
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303546"
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
 *TagName1* OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]] ...  
 Especifica una etiqueta que se va a quitar de un archivo de índice compuesto. Puede eliminar varias etiquetas con un DELETE TAG incluyendo una lista de nombres de etiquetas separados por comas. Si existen dos o más etiquetas con el mismo nombre en los archivos de índice abiertos, puede quitar una etiqueta de un archivo de índice específico incluyendo OF *CDXFileName*.  
  
 TODO [OF *CDXFileName*]  
 Quita todas las etiquetas de un archivo de índice compuesto. Si la tabla actual tiene un archivo de índice compuesto estructural, todas las etiquetas se eliminan del archivo de índice, el archivo de índice se elimina del disco y se elimina el indicador en el encabezado de la tabla que indica la presencia de un archivo de índice compuesto estructural asociado. Utilice ALL con OF *CDXFileName* para quitar todas las etiquetas de un archivo de índice compuesto abierto que no sea el archivo de índice compuesto estructural.  
  
## <a name="remarks"></a>Observaciones  
 Los archivos de índice compuestos, creados con INDEX, contienen etiquetas correspondientes a las entradas de índice. DELETE TAG se utiliza para eliminar una etiqueta o etiquetas de archivos de índice compuesto abiertos. Solo puede eliminar etiquetas de archivos de índice compuesto abiertos en el área de trabajo actual. Si elimina todas las etiquetas de un archivo de índice compuesto, el archivo se elimina del disco.  
  
 Visual FoxPro busca primero una etiqueta en el archivo de índice compuesto estructural (si está abierto). Si la etiqueta no está en el archivo de índice compuesto estructural, Visual FoxPro busca la etiqueta en los otros archivos de índice compuesto abiertos.  
  
## <a name="see-also"></a>Consulte también  
 [Comando de índice](../../odbc/microsoft/index-command.md)
