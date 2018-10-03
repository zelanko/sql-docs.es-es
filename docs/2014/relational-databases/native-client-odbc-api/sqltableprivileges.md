---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 102f8dbaf0746d4f0fd263d7c562b6f74611830c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143965"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
  **SQLTablePrivileges** se puede ejecutar en un cursor estático. Un intento de ejecutar **SQLTablePrivileges** en un cursor actualizable (dinámico o dinámico) devuelve SQL_SUCCESS_WITH_INFO para indicar que el tipo de cursor ha cambiado.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el *CatalogName* parámetro: *nombre_servidor_vinculado.nombre_catálogo*.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLTablePrivileges] (http://go.microsoft.com/fwlink/?LinkId=59373\)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
