---
title: Ejemplo de origen de datos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306526"
---
# <a name="data-source-example"></a>Ejemplo de origen de datos
En equipos que ejecutan Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, la información del origen de datos del equipo se almacena en el registro. Dependiendo de la clave del Registro en la que se almacena la información, el origen de datos se conoce como origen de datos de *usuario* o origen de datos *del sistema.* Los orígenes de datos de usuario se almacenan bajo la clave HKEY_CURRENT_USER y solo están disponibles para el usuario actual. Los orígenes de datos del sistema se almacenan bajo la clave HKEY_LOCAL_MACHINE y pueden ser utilizados por más de un usuario en un equipo. También pueden ser utilizados por los servicios de todo el sistema, que pueden obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en el equipo. Para obtener más información acerca de los orígenes de datos de usuario y del sistema, vea [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Supongamos que un usuario tiene tres orígenes de datos de usuario: Personal e Inventario, que utilizan un DBMS de Oracle; y Payroll, que utiliza un DBMS de Microsoft SQL Server. Los valores del Registro para los orígenes de datos pueden ser:  
  
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
  
 y los valores del Registro para el origen de datos Nómina podrían ser:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
