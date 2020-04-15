---
title: CREATE INDEX (Instrucción CREATE INDEX) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280975"
---
# <a name="create-index-statement"></a>Instrucción CREATE INDEX
La sintaxis de la instrucción CREATE INDEX es:  
  
 CREATE [UNIQUE] INDEX *index-name* ON *nombre-tabla* (*identificador de columna* [ASC][DESC][, identificador de *columna* [ASC][DESC]...]) CON \<lista de *opciones de índice*>  
  
 donde \<la lista de *> de opciones* de índice puede ser: PRIMARY &#124; DISALLOW NULL &#124; IGNORE NULL  
  
 Solo el controlador de Microsoft Access usa las opciones de índice DISALLOW NULL e IGNORE NULL. Los controladores dBASE y Paradox aceptan la sintaxis, pero ignoran la presencia de cualquiera de las opciones.  
  
 Cuando se utiliza el controlador Paradox, la instrucción CREATE INDEX crea archivos de clave principal y archivos secundarios de Paradox.  
  
 Esta instrucción no es compatible con los controladores de Microsoft Excel o Text.
