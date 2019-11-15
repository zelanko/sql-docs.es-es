---
title: Instalación en una máquina virtual de Azure
description: Ejecute las soluciones de ciencia de datos y aprendizaje automático de R y Python en una máquina virtual de SQL Server en la nube de Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aeec25b561822e8083b89e03f0f7e74f40660f7b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727613"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>Instalación de SQL Server Machine Learning Services con R y Python en una máquina virtual de Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede instalar la integración de R y Python con Machine Learning Services en una máquina virtual de SQL Server en Azure, lo que elimina las tareas de instalación y configuración. Cuando se ha implementado la máquina virtual, las características están listas para su uso.
 
Para obtener instrucciones paso a paso, consulte [Aprovisionamiento de una máquina virtual Windows con SQL Server en Azure Portal](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision).

En el paso [establecer la configuración de SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) se agrega aprendizaje automático a la instancia.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>Desbloqueo del firewall

El firewall de la máquina virtual de Azure incluye de forma predeterminada una regla que bloquea el acceso a la red de las cuentas de usuario locales de R.

Debe deshabilitar esta regla para asegurarse de que puede tener acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un cliente de ciencia de datos remoto.  De lo contrario, el código de aprendizaje automático no se puede ejecutar en contextos de cálculo que usen el área de trabajo de la máquina virtual.

Para permitir el acceso desde clientes de ciencia de datos remotos:

1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **Reglas de salida**.
3. Deshabilite la siguiente regla:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar devoluciones de llamada ODBC para clientes remotos

Si tiene previsto que los clientes llamen al servidor deban generar consultas de ODBC como parte de sus soluciones, deberá asegurarse de que el Launchpad puede realizar llamadas a ODBC en nombre del cliente remoto. 

Para ello, debe permitir que las cuentas de trabajo SQL que usan Launchpad puedan iniciar sesión en la instancia. Para obtener más información, vea [Agregar SQLRUserGroup como usuario de base de datos](../security/create-a-login-for-sqlrusergroup.md).

<a name="network"></a>

## <a name="add-network-protocols"></a>Agregar protocolos de red

+ Habilitar las canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo Canalizaciones con nombre en las conexiones entre los equipos cliente y servidor, así como en algunas conexiones de naturaleza interna. Si Canalizaciones con nombre no está habilitado, debe instalarlo y habilitarlo tanto en la máquina virtual de Azure como en cualquier cliente de ciencia de datos que se conecte al servidor.
  
+ Habilitar TCP/IP

  Se necesita TCP/IP en las conexiones de bucle invertido. Si aparece el error "SQL Server no existe o se ha denegado el acceso", habilite TCP/IP en la máquina virtual compatible con la instancia.