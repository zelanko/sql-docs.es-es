---
title: Instrucción CREATE INDEX | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad15ad436b0f34f00acbd75e371e998183f22d2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081909"
---
# <a name="create-index-statement"></a>Instrucción CREATE INDEX
La sintaxis de la instrucción CREATE INDEX es la siguiente:  
  
 CREATE [UNIQUE] index *index-Name* en *TABLE-Name* (*identificador de columna* [asc] [Desc] [, *identificador de columna* [asc] [Desc]...]) \< *Lista de opciones* de with index>  
  
 donde \<la *lista de opciones de índice*> puede ser: principal &#124; no permitir null &#124; omitir null  
  
 Solo el controlador de Microsoft Access usa las opciones Disallow NULL e IGNORE NULL index. Los controladores dBASE y Paradox aceptan la sintaxis, pero omiten la presencia de ambas opciones.  
  
 Cuando se usa el controlador de Paradox, la instrucción CREATE INDEX crea archivos de clave principal y archivos secundarios de Paradox.  
  
 Esta instrucción no es compatible con los controladores de texto o de Microsoft Excel.
