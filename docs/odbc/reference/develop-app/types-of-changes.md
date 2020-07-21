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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301610"
---
# <a name="types-of-changes"></a>Tipos de cambios
Se realizan tres tipos de cambios en ODBC *3. x* (y cualquier versión de ODBC). Cada uno de ellos afecta a la compatibilidad con versiones anteriores de forma diferente y se administra de forma diferente. Estos cambios se describen en la tabla siguiente.  
  
|Tipo de cambio|Descripción|  
|--------------------|-----------------|  
|Características nuevas|Se trata de características que son nuevas en ODBC *3. x*, como los enlaces o descriptores fuera de línea. Solo se implementan cuando la aplicación y el controlador, así como el administrador de controladores, son de la versión *3. x*, por lo que no se intenta hacer que sean compatibles con versiones anteriores.|  
|Características duplicadas|Se trata de características que existen en ODBC *2. x* y en ODBC *3. x* , pero se implementan de maneras diferentes en cada una de ellas. Las funciones **SQLAllocHandle** y **SQLAllocStmt** son un ejemplo. Los problemas de compatibilidad con versiones anteriores de estas y otras características duplicadas se controlan principalmente mediante asignaciones en el administrador de controladores.|  
|Cambios de comportamiento|Se trata de características que se administran de forma diferente en ODBC *2. x* y en ODBC *3. x*. Un **#define** DateTime es un ejemplo. Estas características se controlan mediante el controlador ODBC *3. x* en función de un valor de atributo de entorno. (Vea [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información).|
