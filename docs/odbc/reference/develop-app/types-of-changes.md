---
title: Tipos de cambios ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301610"
---
# <a name="types-of-changes"></a>Tipos de cambios
Se realizan tres tipos de cambios en ODBC *3.x* (y en cualquier versión de ODBC). Cada uno de ellos afecta a la compatibilidad con versiones anteriores de forma diferente y se controla de una manera diferente. Estos cambios se describen en la tabla siguiente.  
  
|Tipo de cambio|Descripción|  
|--------------------|-----------------|  
|Características nuevas|Estas son características que son nuevas para ODBC *3.x*, como el enlace fuera de línea o descriptores. Estos se implementan sólo cuando la aplicación y el controlador, así como el Administrador de controladores, son de la versión *3.x,* por lo que no hay ningún intento de hacerlos compatibles con versiones anteriores.|  
|Funciones duplicadas|Estas son características que existen en ODBC *2.x* y ODBC *3.x,* pero se implementan de diferentes maneras en cada uno. Las funciones **SQLAllocHandle** y **SQLAllocStmt** son un ejemplo. Los problemas de compatibilidad con versiones anteriores para estas y otras características duplicadas se controlan principalmente mediante asignaciones en el Administrador de controladores.|  
|Cambios de comportamiento|Estas son características que se controlan de forma diferente en ODBC *2.x* y ODBC *3.x*. Un **#define** datetime es un ejemplo. Estas características se controlan mediante el controlador ODBC *3.x* en función de una configuración de atributo de entorno. (Consulte [Cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)|
