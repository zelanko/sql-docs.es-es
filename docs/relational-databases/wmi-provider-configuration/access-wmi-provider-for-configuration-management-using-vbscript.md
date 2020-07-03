---
title: Obtener acceso al proveedor WMI con VBScript
description: Obtenga información acerca de cómo crear un programa de VBScript que muestre la versión de las instancias instaladas de SQL Server que se ejecutan en un equipo.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab864d3e2fbfb10e98347ac40b0b5f74f08729cb
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888236"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>Acceso al proveedor WMI para la administración de configuración mediante VBScript
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En esta sección se describe cómo crear un programa de VBScript que muestre la versión de las instancias instaladas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en un equipo.  
  
 En el ejemplo de código se muestran las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en el equipo y su versión.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Mostrar el nombre y la versión de las instancias instaladas de SQL Server  
  
1.  Abra un nuevo documento en un editor de texto, como el Bloc de notas de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copie el código incluido después de este procedimiento y guarde el archivo con la extensión .vbs. Este ejemplo se denomina test.vbs.  
  
2.  Conéctese a una instancia del proveedor WMI para la Administración de equipos con la función de VBScript `GetObject`. Este ejemplo se conecta a un equipo remoto denominado mpc, pero omita el nombre de equipo para conectarse al equipo local: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Para obtener más información sobre la función `GetObject`, vea la referencia de VBScript.  
  
3.  Utilice el método `InstancesOf` para mostrar una lista de los servicios. Los servicios también se pueden mostrar mediante una consulta WQL simple y un método `ExecQuery` en lugar del método `InstancesOf`.  
  
4.  Utilice el método `ExecQuery` y una consulta WQL para recuperar el nombre y la versión de las instancias instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Guarde el archivo.  
  
6.  Ejecute el script escribiendo **cscript test. vbs** en el símbolo del sistema.  

## <a name="example"></a>Ejemplo  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
