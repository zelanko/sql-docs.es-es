---
title: 'Instale el lenguaje R y las características de Python en una máquina virtual de Azure: SQL Server Machine Learning Services'
description: Ejecutar soluciones en una máquina virtual de SQL Server en la nube de Azure de aprendizaje automático y ciencia de datos de R y Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 551d7c81220175efd1143323cce0a9bcdb4ad3f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962903"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instale SQL Server Machine Learning Services con R y Python en una máquina virtual de Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede instalar la integración de R y Python con Machine Learning Services en una máquina virtual de SQL Server en Azure, lo que elimina las tareas de instalación y configuración. Una vez implementada la máquina virtual, están listos para usar las características.
 
Para obtener instrucciones paso a paso, consulte [cómo aprovisionar una máquina virtual de Windows SQL Server en Azure portal](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

El [configuración de configurar SQL server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) paso consiste en Agregar aprendizaje automático a la instancia.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloquear el firewall

De forma predeterminada, el firewall de la máquina virtual de Azure incluye una regla que bloquea el acceso a las cuentas de usuario local de red.

Debe deshabilitar esta regla para asegurarse de que puede tener acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia desde un cliente de ciencia de datos remoto.  En caso contrario, no se puede ejecutar el código de aprendizaje automático en contextos de proceso que use el área de trabajo de la máquina virtual.

Para habilitar el acceso desde clientes de ciencia de datos remoto:

1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **Reglas de salida**.
3. Deshabilite la siguiente regla:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar devoluciones de llamada ODBC para clientes remotos

Si espera que los clientes que llamen al servidor deberá emitir consultas ODBC como parte de su soluciones de aprendizaje automático, debe asegurarse de que el Launchpad puede realizar llamadas ODBC en nombre del cliente remoto. 

Para ello, debe permitir que las cuentas de trabajo SQL que usan Launchpad puedan iniciar sesión en la instancia. Para obtener más información, consulte [agregar SQLRUserGroup como un usuario de base de datos](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Agregar protocolos de red

+ Habilitar las canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo Canalizaciones con nombre en las conexiones entre los equipos cliente y servidor, así como en algunas conexiones de naturaleza interna. Si Canalizaciones con nombre no está habilitado, debe instalarlo y habilitarlo tanto en la máquina virtual de Azure como en cualquier cliente de ciencia de datos que se conecte al servidor.
  
+ Habilitar TCP/IP

  Es necesaria para las conexiones de bucle invertido TCP/IP. Si se produce el error "DBNETLIB SQL Server no existe o acceso denegado", habilite TCP/IP en la máquina virtual compatible con la instancia.