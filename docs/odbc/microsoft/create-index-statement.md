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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280975"
---
# <a name="create-index-statement"></a>Instrucción CREATE INDEX
La sintaxis de la instrucción CREATE INDEX es la siguiente:  
  
 CREATE [UNIQUE] index *index-Name* en *TABLE-Name* (*identificador de columna* [asc] [Desc] [, *identificador de columna* [asc] [Desc]...]) \< *Lista de opciones* de with index>  
  
 donde \<la *lista de opciones de índice*> puede ser: principal &#124; no permitir null &#124; omitir null  
  
 Solo el controlador de Microsoft Access usa las opciones Disallow NULL e IGNORE NULL index. Los controladores dBASE y Paradox aceptan la sintaxis, pero omiten la presencia de ambas opciones.  
  
 Cuando se usa el controlador de Paradox, la instrucción CREATE INDEX crea archivos de clave principal y archivos secundarios de Paradox.  
  
 Esta instrucción no es compatible con los controladores de texto o de Microsoft Excel.
