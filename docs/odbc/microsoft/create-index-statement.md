---
description: Instrucción CREATE INDEX
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
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483638"
---
# <a name="create-index-statement"></a>Instrucción CREATE INDEX
La sintaxis de la instrucción CREATE INDEX es la siguiente:  
  
 CREATE [UNIQUE] index *index-Name* en *TABLE-Name* (*identificador de columna* [asc] [Desc] [, *identificador de columna* [asc] [Desc]...]) Gracias \<*index option list*>  
  
 donde \<*index option list*> puede ser: primary &#124; no permitir valores null &#124; ignore null  
  
 Solo el controlador de Microsoft Access usa las opciones Disallow NULL e IGNORE NULL index. Los controladores dBASE y Paradox aceptan la sintaxis, pero omiten la presencia de ambas opciones.  
  
 Cuando se usa el controlador de Paradox, la instrucción CREATE INDEX crea archivos de clave principal y archivos secundarios de Paradox.  
  
 Esta instrucción no es compatible con los controladores de texto o de Microsoft Excel.
