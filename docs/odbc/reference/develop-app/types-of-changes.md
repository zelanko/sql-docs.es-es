---
title: Tipos de cambios | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac92c6d40ea9ead6b8875e3338bb740b4bdf8523
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631823"
---
# <a name="types-of-changes"></a>Tipos de cambios
Tres tipos de cambios se realizan en ODBC 3. *x* (y cualquier versión de ODBC). Cada una de ellas afecta a la compatibilidad con versiones anteriores de manera diferente y se controla de manera diferente. Estos cambios se describen en la tabla siguiente.  
  
|Tipo de cambio|Descripción|  
|--------------------|-----------------|  
|Nuevas características|Éstas son características que son nuevas en ODBC 3. *x*, tales como enlace fuera de línea o de descriptores. Estos elementos se implementan solo cuando la aplicación y controlador, así como el Administrador de controladores, son de versión 3 *.x*, por lo que no hay ningún intento para hacer que estas sea compatible con versiones anteriores.|  
|Características duplicados|Estas son las características que existen en ODBC 2 *.x* mientras que ODBC 3. *x* pero se implementan de maneras diferentes en cada uno. Las funciones **SQLAllocHandle** y **SQLAllocStmt** son un ejemplo. Problemas de compatibilidad con versiones anteriores para estas y otras características duplicados se controlan principalmente por asignaciones en el Administrador de controladores.|  
|Cambios de comportamiento|Estas son las características que se controlan de forma diferente de ODBC 2 *.x* mientras que ODBC 3. *x*. Un valor datetime **#define** es un ejemplo. Estas características se controlan mediante el ODBC 3. *x* controlador según un valor de atributo de entorno. (Consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)|
