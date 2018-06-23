---
title: Modificar servicio propiedades avanzadas SQL Server mediante VBScript | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 003755ca5366a8571cdcb63f0c59c51a8012bb11
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198131"
---
# <a name="modify-sql-server-service-advanced-properties-using-vbscript"></a>Modificar propiedades avanzadas de servicios SQL Server mediante VBScript
  En esta sección se describe cómo crear un programa de VBScript que muestra la versión de las instancias instaladas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en un equipo.  
  
 En el ejemplo de código se muestran las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecutan en el equipo y su versión.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Mostrar el nombre y la versión de las instancias instaladas de SQL Server  
  
1.  Abra un nuevo documento en un editor de texto, como el Bloc de notas de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copie el código incluido después de este procedimiento y guarde el archivo con la extensión .vbs. Este ejemplo se denomina test.vbs.  
  
2.  Conéctese a una instancia del proveedor WMI para la Administración de equipos con la función de VBScript `GetObject`. Este ejemplo se conecta a un equipo remoto denominado mpc, pero omita el nombre de equipo para conectarse al equipo local: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Para obtener más información sobre la función `GetObject`, vea la referencia de VBScript.  
  
3.  Utilice el método `InstancesOf` para mostrar una lista de los servicios. Los servicios también se pueden mostrar mediante una consulta WQL simple y un método `ExecQuery` en lugar del método `InstancesOf`.  
  
4.  Utilice el método `ExecQuery` y una consulta WQL para recuperar el nombre y la versión de las instancias instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Guarde el archivo.  
  
6.  Ejecute la secuencia de comandos escribiendo `cscript test.vbs` en el símbolo del sistema.  
  
## <a name="example"></a>Ejemplo  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  