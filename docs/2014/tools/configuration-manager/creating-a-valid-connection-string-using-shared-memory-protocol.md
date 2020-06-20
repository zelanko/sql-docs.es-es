---
title: Crear una cadena de conexión válida con el protocolo de memoria compartida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0add5ea97f6a07f177dd844bd840d88145f81b2a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057956"
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>Crear una cadena de conexión válida con el protocolo de memoria compartida
  Las conexiones a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un cliente que se ejecuta en el mismo equipo utilizan el protocolo de memoria compartida. La memoria compartida no tiene propiedades que se puedan configurar. Memoria compartida es el protocolo que se intenta utilizar en primer lugar y no se puede desplazar de la posición prioritaria de la lista **Protocolos habilitados** de la lista **Propiedades de los protocolos de cliente** . El protocolo de memoria compartida se puede deshabilitar, lo que resulta útil para solucionar problemas con los demás protocolos.  
  
 No es posible crear un alias con el protocolo de memoria compartida, pero si el protocolo está habilitado, al conectarse al [!INCLUDE[ssDE](../../includes/ssde-md.md)] por nombre se crea una conexión de memoria compartida. Una cadena de conexión de memoria compartida usa el formato `lpc:<servername>[\instancename]`.  
  
## <a name="connecting-to-the-local-server"></a>Conectarse al servidor local  
 Al conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se ejecuta en el mismo equipo que el cliente, puede usar **(local)** como nombre de servidor. Esta posibilidad no se recomienda ya que genera ambigüedad, pero puede ser útil cuando se sabe que el cliente se ejecuta en el equipo de destino. Por ejemplo, al crear una aplicación para usuarios desconectados móviles, como puede ser el personal de ventas, en la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutará en equipos portátiles y se almacenarán datos de proyectos, un cliente que se conecte a **(local)** siempre se conectará al servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en el equipo portátil. En lugar de **(local)** , se puede usar la palabra**localhost**o un punto ( **.** ).  
  
## <a name="verifying-your-connection-protocol"></a>Comprobar el protocolo de conexión  
 La siguiente consulta devolverá el protocolo utilizado para la conexión actual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Ejemplos:  
 Los siguientes nombres se conectarán al equipo local con el protocolo de memoria compartida si está habilitado:  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 No se puede crear un alias para una conexión de memoria compartida.  
  
> [!NOTE]  
>  Si se especifica una dirección IP en el cuadro **Servidor** , se establecerá una conexión TCP/IP.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una cadena de conexión válida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Crear una cadena de conexión válida con canalizaciones con nombre](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
