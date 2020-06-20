---
title: Características de ejecución de procedimientos almacenados extendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.openlocfilehash: 62c95f0cb6c8239fee86b27b231e3e1830fb5009
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050904"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>Características de ejecución de los procedimientos almacenados extendidos
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 La ejecución de un procedimiento almacenado extendido tiene estas características:  
  
-   La función de procedimiento almacenado extendido se ejecuta en el contexto de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La función de procedimiento almacenado extendido se ejecuta en el espacio de procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El subproceso asociado a la ejecución del procedimiento almacenado extendido es el mismo que se utiliza para la conexión de cliente.  
  
    > [!IMPORTANT]  
    >  Antes de agregar procedimientos almacenados extendidos al servidor y otorgar permisos de ejecución a otros usuarios, el administrador del sistema debe revisar por completo cada procedimiento almacenado extendido para asegurarse de que no contiene código perjudicial o dañino.  
  
-  
  
 Una vez cargado el archivo DLL de procedimiento almacenado extendido, el archivo DLL permanece cargado en el espacio de direcciones del servidor hasta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene o el administrador descarga explícitamente el archivo DLL mediante DBCC *DLL_name* (Free).  
  
 El procedimiento almacenado extendido se puede ejecutar desde [!INCLUDE[tsql](../../includes/tsql-md.md)] como un procedimiento almacenado utilizando la instrucción EXECUTE:  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parámetros  
 \@ *retval*  
 Es un valor devuelto.  
  
 \@*parám1*  
 Es un parámetro de entrada.  
  
 \@*parám2*  
 Es un parámetro de entrada/salida.  
  
> [!CAUTION]  
>  Los procedimientos almacenados extendidos proporcionan mejoras de rendimiento y amplían la funcionalidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, como la DLL de procedimiento almacenado extendido y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comparten el mismo espacio de direcciones, un procedimiento con problemas puede afectar de forma negativa al funcionamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra las excepciones generadas por la DLL de procedimiento almacenado extendido, es posible que las áreas de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resulten dañadas. Como medida de seguridad preventiva, solo los administradores del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden agregar los procedimientos almacenados extendidos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de instalar estos procedimientos, se deberían probar con detenimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Programar procedimientos almacenados extendidos](database-engine-extended-stored-procedures-programming.md)   
 [Consultar procedimientos almacenados extendidos instalados en SQL Server](querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
