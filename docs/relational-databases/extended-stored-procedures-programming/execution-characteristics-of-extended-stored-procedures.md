---
title: Características de ejecución de procedimientos almacenados extendidos
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 74ecd20f28e58e133b5710d3cbd9d18b27ca7756
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095987"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>Características de ejecución de los procedimientos almacenados extendidos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]En su lugar, use la integración con CLR.  
  
 La ejecución de un procedimiento almacenado extendido tiene estas características:  
  
-   La función de procedimiento almacenado extendido se ejecuta en el contexto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]seguridad de.  
  
-   La función de procedimiento almacenado extendido se ejecuta en el espacio de procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El subproceso asociado a la ejecución del procedimiento almacenado extendido es el mismo que se utiliza para la conexión de cliente.  
  
    > [!IMPORTANT]  
    >  Antes de agregar procedimientos almacenados extendidos al servidor y otorgar permisos de ejecución a otros usuarios, el administrador del sistema debe revisar por completo cada procedimiento almacenado extendido para asegurarse de que no contiene código perjudicial o dañino.  
  
-  
  
 Una vez cargado el archivo DLL de procedimiento almacenado extendido, el archivo DLL permanece cargado en el espacio de direcciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servidor hasta que se detiene o el administrador descarga explícitamente el archivo DLL mediante DBCC *DLL_name* (Free).  
  
 El procedimiento almacenado extendido se puede ejecutar desde [!INCLUDE[tsql](../../includes/tsql-md.md)] como un procedimiento almacenado utilizando la instrucción EXECUTE:  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>Parámetros  
 \@*retval*  
 Es un valor devuelto.  
  
 \@*parám1*  
 Es un parámetro de entrada.  
  
 \@*parám2*  
 Es un parámetro de entrada/salida.  
  
> [!CAUTION]  
>  Los procedimientos almacenados extendidos proporcionan mejoras de rendimiento y amplían la funcionalidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, como la DLL de procedimiento almacenado extendido y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comparten el mismo espacio de direcciones, un procedimiento con problemas puede afectar de forma negativa al funcionamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra las excepciones generadas por la DLL de procedimiento almacenado extendido, es posible que las áreas de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resulten dañadas. Como medida de seguridad preventiva, solo los administradores del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden agregar los procedimientos almacenados extendidos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de instalar estos procedimientos, se deberían probar con detenimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Programar procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [Consultar procedimientos almacenados extendidos instalados en SQL Server](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
