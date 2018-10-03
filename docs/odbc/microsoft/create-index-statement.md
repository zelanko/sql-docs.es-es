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
manager: craigg
ms.openlocfilehash: 93ddc3881796aee3194ec5268afc68ecbab1a487
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782893"
---
# <a name="create-index-statement"></a>Instrucción CREATE INDEX
La sintaxis de la instrucción CREATE INDEX es:  
  
 Crear índice [UNIQUE] *nombre del índice* ON *nombre-tabla* (*identificador de columna* [ASC] [DESC] [, *identificador de columna* [ASC][DESC]...]) CON \< *lista de opciones de índice*>  
  
 donde \< *lista de opciones de índice*> puede ser: principal &#124; DISALLOW NULL &#124; IGNORE NULL  
  
 Solo el controlador de Microsoft Access utiliza las opciones de índice no permitir NULL e IGNORE NULL. Los controladores de Paradox y dBASE aceptan la sintaxis, pero omitir la presencia de cualquiera de las opciones.  
  
 Cuando se usa el controlador de Paradox, la instrucción CREATE INDEX crea Paradox archivos de clave principales y secundaria.  
  
 Esta instrucción no es compatible con los controladores de Microsoft Excel o texto.
