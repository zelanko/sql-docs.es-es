---
description: Cursores mixtos
title: Cursores mixtos | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b15aaee9d74319daa1a211610ce283d247fda2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424607"
---
# <a name="mixed-cursors"></a>Cursores mixtos

Un cursor mixto es una combinación de un cursor controlado por conjunto de claves y un cursor dinámico. Se usa cuando el conjunto de resultados es demasiado grande para guardar las claves de forma razonable para todo el conjunto de resultados. Los cursores mixtos se implementan mediante la creación de un conjunto de claves menor que el conjunto de resultados completo pero mayor que el conjunto de filas.  
  
 Siempre y cuando la aplicación se desplace dentro del conjunto de claves, el comportamiento es controlado por conjunto de claves. Cuando la aplicación se desplaza fuera del conjunto de claves, el comportamiento es dinámico: el cursor captura las filas solicitadas y crea un nuevo conjunto de claves. Una vez creado el nuevo conjunto de claves, el comportamiento se revierte a controlado por conjunto de claves dentro de ese conjunto de claves.  
  
 Por ejemplo, suponga que un conjunto de resultados tiene 1.000 filas y utiliza un cursor mixto con un tamaño de conjunto de claves de 100 y un tamaño de conjunto de filas de 10. Cuando se captura el primer conjunto de filas, el cursor crea un conjunto de claves que se compone de las claves de las primeras 100 filas. Después, devuelve las 10 primeras filas, tal y como se solicitó.  
  
 Ahora Supongamos que otra aplicación elimina las filas 11 y 101. Si el cursor intenta recuperar la fila 11, se producirá un hueco porque tiene una clave para esta fila pero no existe ninguna fila. se trata de un comportamiento controlado por conjunto de claves. Si el cursor intenta recuperar la fila 101, el cursor no detectará que falta la fila porque no tiene una clave para la fila. En su lugar, se recuperará lo que era anterior fila 102. Este es el comportamiento de cursor dinámico.  
  
 Un cursor mixto es equivalente a un cursor controlado por conjunto de claves cuando el tamaño del conjunto de claves es igual al tamaño del conjunto de resultados. Un cursor mixto es equivalente a un cursor dinámico cuando el tamaño del conjunto de claves es igual a 1.
