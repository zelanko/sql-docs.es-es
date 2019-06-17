---
title: Use la ruta de acceso completa para registrar nombres de DLL de procedimiento almacenado extendido | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- registering DLL names
- extended stored procedures [SQL Server], registering
- DLL names [SQL Server]
- full path DLL name registration [SQL Server]
ms.assetid: f648d57c-af32-4c71-9882-47b6766f3c2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e560ec0fd617d4da46235803da8cbd69ef4f80d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091288"
---
# <a name="use-the-full-path-to-register-extended-stored-procedure-dll-names"></a>Utilizar la ruta de acceso completa para registrar nombres de DLL de procedimiento almacenado extendido
  Es posible que los procedimientos almacenados extendidos registrados anteriormente sin la ruta de acceso completa para el nombre de DLL no funcionen en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Es posible que los procedimientos almacenados extendidos registrados anteriormente sin la ruta de acceso completa para el nombre de DLL no funcionen después de realizar la actualización. Esto se debe a que, durante el proceso de actualización, no se agrega el antiguo directorio BINN a la nueva ruta de acceso. Es posible que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueda encontrar los procedimientos almacenados extendidos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar, siga estos pasos para cada procedimiento almacenado extendido que no se haya registrado con un nombre completo de ruta de acceso:  
  
1.  Ejecute sp_dropextendedproc para quitar el procedimiento almacenado extendido.  
  
2.  Ejecute sp_addextendedproc para registrar el procedimiento almacenado extendido con el nombre completo de ruta de acceso.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
