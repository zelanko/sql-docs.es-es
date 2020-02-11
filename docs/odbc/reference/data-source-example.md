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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135636"
---
# <a name="data-source-example"></a>Ejemplo de origen de datos
En los equipos que ejecutan Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, la información del origen de datos de la máquina se almacena en el registro. En función de la clave del registro en la que se almacene la información, el origen de datos se denomina origen de datos del *usuario* o origen de *datos del sistema*. Los orígenes de datos de usuario se almacenan en la clave HKEY_CURRENT_USER y solo están disponibles para el usuario actual. Los orígenes de datos del sistema se almacenan con la clave HKEY_LOCAL_MACHINE y pueden ser usados por más de un usuario en un equipo. También pueden utilizarlos los servicios de todo el sistema, que pueden obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en la máquina. Para obtener más información acerca de los orígenes de datos de usuario y del sistema, vea [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Supongamos que un usuario tiene tres orígenes de datos de usuario: personal e inventario, que usan un DBMS de Oracle. y Payroll, que utiliza un DBMS Microsoft SQL Server. Los valores del registro para los orígenes de datos pueden ser:  
  
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
