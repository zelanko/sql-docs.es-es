---
title: Instalación en una máquina virtual de Azure
description: Ejecute soluciones de ciencia de datos y aprendizaje automático de Python y R con SQL Server Machine Learning Services en una máquina virtual en la nube de Azure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d81237f67c82fd7cc8b9259fcd7a0202ffb7fd4b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75776596"
---
# <a name="install-sql-server-machine-learning-services-with-python-and-r-on-an-azure-virtual-machine"></a>Instalación de SQL Server Machine Learning Services con Python y R en una máquina virtual de Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Aprenda a instalar Python y R con SQL Server Machine Learning Services en una máquina virtual de Azure. Esto elimina las tareas de instalación y configuración de Machine Learning Services.

Siga estos pasos:

1. Aprovisionamiento de una máquina virtual de SQL Server en Azure
1. Desbloqueo del firewall
1. Habilitar devoluciones de llamada ODBC para clientes remotos
1. Agregar protocolos de red

## <a name="provision-sql-server-virtual-machine-in-azure"></a>Aprovisionamiento de una máquina virtual de SQL Server en Azure

Para obtener instrucciones paso a paso, consulte [Aprovisionamiento de una máquina virtual Windows con SQL Server en Azure Portal](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision). 

El paso [Configuración de SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) es donde se agrega Machine Learning Services a la instancia.

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