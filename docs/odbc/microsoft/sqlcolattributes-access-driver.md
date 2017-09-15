---
title: SQLColAttributes (controlador de acceso) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2531bbc58e55c3c58452701f1dd66ac6702a535
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attribute|Comentarios|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Para los datos LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE es la longitud máxima de la columna, no la longitud máxima de la columna horas 2.|  
|SQL_OWNER_NAME|Una cadena vacía ("") se devuelve en esta columna porque no se admite el nombre del propietario.|  
|SQL_QUALIFIER_NAME|Se devuelve la ruta de acceso a un archivo de base de datos.|  
|SQL_COLUMN_SEARCHABLE|Columnas LONGVARBINARY y LONGVARCHAR se notifican como SQL_UNSEARCHABLE.<br /><br /> Tipos de datos de caracteres y binarios de longitud fija y de longitud variable son permite realizar búsquedos, aunque no sean LONGVARBINARY y LONGVARCHAR.|  
  
> [!NOTE]  
>  Los pasos anteriores no es una lista completa de los atributos devueltos por **SQLColAttributes**.
