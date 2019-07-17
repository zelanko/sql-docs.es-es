---
title: Ejemplo de origen de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec9eacef6f0bd63eb0aaeac36dc97938297d1f16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135636"
---
# <a name="data-source-example"></a>Ejemplo de origen de datos
Los equipos que ejecutan Microsoft® Windows NT® Server o Windows 2000 Server, Microsoft Windows NT Workstation o Windows 2000 Professional o Microsoft Windows® 95/98, datos de la máquina en el registro se almacena la información de origen. Dependiendo de qué registro de la clave se almacena en la información, el origen de datos se conoce como un *origen de datos de usuario* o un *origen de datos del sistema*. Orígenes de datos de usuario se almacenan bajo la clave HKEY_CURRENT_USER y solo están disponibles para el usuario actual. Orígenes de datos del sistema se almacenan bajo la clave HKEY_LOCAL_MACHINE y pueden usarse por más de un usuario en un solo equipo. También puede usarse por los servicios de todo el sistema, que, a continuación, se pueden obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en la máquina. Para obtener más información acerca de los orígenes de datos del sistema y de usuario, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Supongamos que un usuario tiene tres orígenes de datos de usuario: Personal e inventario, que usan un DBMS que Oracle; y nóminas, que usa un DBMS de Microsoft SQL Server. Los valores del registro de orígenes de datos podrían ser:  
  
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
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
