---
title: Ejemplo de origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7d80fc111164b2f32a1394f214dc09c3f61c51c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="data-source-example"></a>Ejemplo de origen de datos
Equipos que ejecutan Microsoft® Windows NT® Server o Windows 2000 Server, Microsoft Windows NT Workstation o Windows 2000 Professional o Microsoft Windows® 95 ó 98, datos de la máquina se almacena la información de origen en el registro. Dependiendo de qué registro clave se almacena la información en, el origen de datos se conoce como un *origen de datos de usuario* o un *origen de datos del sistema*. Orígenes de datos de usuario se almacenan en la clave HKEY_CURRENT_USER y solo están disponibles para el usuario actual. Orígenes de datos del sistema se almacenan en la clave HKEY_LOCAL_MACHINE y pueden usarse por más de un usuario en un equipo. También pueden ser usados por servicios de todo el sistema, que, a continuación, se pueden obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en el equipo. Para obtener más información sobre orígenes de datos del sistema y de usuario, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Supongamos que un usuario tiene tres orígenes de datos de usuario: personal y el inventario, que utiliza un DBMS que Oracle; y nómina, que utiliza un DBMS de Microsoft SQL Server. Los valores del registro para los orígenes de datos pueden ser:  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 y los valores del registro para el origen de datos de nóminas podrían ser:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
