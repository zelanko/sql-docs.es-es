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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 03c19fecd314bd67949b133e6c1e0ae9e8292d3d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705858"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
  **SQLTablePrivileges** se puede ejecutar en un cursor estático. Un intento de ejecutar **SQLTablePrivileges** en un control actualizable (controlado por conjunto de claves o dinámico) devuelve SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte también  
 [SQLTablePrivileges función] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
