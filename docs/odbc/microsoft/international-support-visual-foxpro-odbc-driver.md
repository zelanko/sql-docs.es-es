---
title: Compatibilidad internacional (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f99c63f641ecdb6338f8028cc7438021e32e2ae
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Compatibilidad internacional (controlador ODBC de Visual FoxPro)
Es compatible con el controlador ODBC de Microsoft Visual FoxPro:  
  
-   Juegos de caracteres de doble byte (DBCS)  
  
-   Varias secuencias de intercalación  
  
 Una secuencia de intercalación define el *criterio de ordenación* para los datos almacenados en una tabla de Visual FoxPro o una base de datos. De forma predeterminada, el controlador está configurado para utilizar las secuencias de intercalación que admiten la versión de idioma del sistema operativo.  
  
 Para obtener una lista de secuencias de intercalación admitidas, consulte [establecer COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>configuración regional  
 El conjunto de información que corresponde a un determinado idioma y país o región. Una configuración regional indica opciones específicas como separadores decimales, fecha y formatos de hora y orden de clasificación de caracteres.  
  
## <a name="sort-order"></a>criterio de ordenación  
 Criterios de ordenación incorporan las reglas de ordenación de diferentes *configuración regional*s, lo que le permite ordenar los datos en esos idiomas correctamente. En Visual FoxPro, el criterio de ordenación actual determina los resultados de las comparaciones de expresión de caracteres y el orden en que aparecen en los registros de la indización u ordenar tablas.
